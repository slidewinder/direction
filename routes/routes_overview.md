# slidewinder UX interaction routes

This document lays out the routes users can take when interacting with slidewinder. It is used to develop the spec for the API, and to design the user interfaces.


## route `home`

> slidewinder `{{version}}` `{{logo}}`

if (!`setup`) -> route `intial_setup`

**what would you like to do?**

- create a slide [-> route `search_slides`]
- create a deck [-> route `create deck`]
- present a deck [-> route `present deck`]
- manage your slide library [-> route `manage library`]
- get help [-> route `help`]
- exit [-> route `exit`]

## route `intial_setup`

> It looks like this is your first time using slidewinder.
Let's get you set up - it won't take long.

- ? your name -> `string`
- ? where would you like to store slides by default? ->
    `string` directory chooser

(set setup=true in global config)

> that's all we need for now, taking you back to slidewinder
  - [home -> route `home`]

## route `create_slide`

**create a new slide**

- ? title -> `string`
- ? author (suggest default) `string`
- ? style -> (choose slide generator template)
- ? content -> based on template

[choices]:
- preview [-> `slide.render` -> `open`]
- save [-> `slide.flush`]
- done [-> `slide.flush` -> route `home`]
- save and make another [-> `slide.flush` -> route `create_slide`]

## route `create_deck`

**create a new deck**

- ? name
- ? author (suggest default)
- ? slides ->
  - find a slide [-> route `search_slides`]
  - make a slide [-> route `create_slide`]

## route `present_deck`

**present a deck**

> search for the deck you want to present: [-> route `search_decks`]

options ?? <- decide what these are
- remote control options?

present -> generate deck and open in browser | cancel

## route `manage_library`

**manage library**

What would you like to do?
- create a collection [-> route `create_collection`]
- manage existing collections [-> route `search_collections`]
- manage slides [-> route `search_slides`[

## route `search_collections`

**search collections**

if !collections:
You don't have any collections yet.
else:

Start typing to search your collections.

- dynamic list based on query

when user selects a result [-> route `collection_view`]

## route `collection_view`

metadata fields are isplayed as a table, with some summary stats
like number of slides etc.

metadata fields can be edited and saved

searchable list of slides (with a limit to how many are displayed)
when a slide is selected the user can choose to remove it from the collection

## route `help`

slidewinder {{version}} {{logo}} help

How can we help?

1. learn how to use slidewinder [-> `open` docs website]
2. chat to slidewinder users and team [-> `open` gitter room]
3. report a bug [-> `open` github issues]

## route `search_slides`

**search your slide library**

Start typing to search

> show dynamic list of slides matchinf query with a limit
> can page through results
> arrow keys select a slide, enter shows a menu for that slide
> individual slide menu allows:
- edit -> route `edit_slide`
- add tags -> provide a field to add (autocompleted) tags
- add to collection -> provide a field to enter (autocompleted) collection
- create a new deck with this slide -> route `new_deck`
- select

[choices]:
  - OK [-> `route callback` selected slide IDs]
  - cancel [-> `route callback` null]

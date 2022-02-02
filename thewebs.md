# thewebs
## What Is It?
Basically just a bookmark manager, will be highly inspired by https://superdense.com. Compact, fully-featured, reliable, and accessable everywhere at any time, I hope.

- Superdense pics
	![homepage](_attachments/Pasted%20image%2020220202131344.png)
	![pricing page](_attachments/Pasted%20image%2020220202131642.png)
	![so called promo page](_attachments/Pasted%20image%2020220202131726.png)
	![app page](_attachments/Pasted%20image%2020220202131524.png)

## Why build this?
I will build this insyaa Allah because I like the idea of simple bookmark manager and currently can't afford Superdense (but I'll more likely build it myself if I afford it, tho).

## Features
### Structure 
- a bookmark
	- has categories
		- has webs
			- has URL, favicon, title, categories (many to many relationship)
### Functional
#### Bookmarks
##### CRUD
###### Create
- Users will be able to save a URL to their bookmarks
	- and the app will save the URL and the Favicon
	- ...and generate a title based on the URL given
		- which users will be able to edit if the title is not fit them
	- also will be placed in the corresponding categories by user
- Users will be able to create categories for their bookmarks
###### Update & Delete
- Users will be able to edit and delete their bookmarks
	- Editable: URL, Favicon (upload own img/svg/ico), title
###### Read
- Users will be given a URL that redirects to a webpage displaying all their bookmarks
	- There will be two webs and thus two URLs
		- a web showing public bookmarks
		- and a web showing private bookmarks
			- which require login to access them
		- Users will be able to set a **category** to be private or public (**not per URL**)

##### Sharing
- Users will be able to add/invite another users to see and (if allowed) edit their private bookmarks

#### Users
- New users will be able to register using their Email, Gmail, Twitter, Facebook, etc. (or just email suffice imo)
- Users will be able to login using email and password (and other credentials above)
	- maybe implement forgot password condition
		- require email sending


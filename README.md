#What is cVim?

Vim for Google Chrome. I hate using the mouse, especially after learning Vim. With my desktop (Linux), I have a lot of key bindings that make doing things easier: I open Chrome with `Alt+w`, I close a window with `Alt+Shift+d`, I open a terminal with `Alt+t`. This is harder to do with Chrome because it has no section for customizing keyboard shortcuts, and it is still necessary to use the mouse to do things like click links. cVim aims to eliminate this problem as best as the Chrome extensions API will allow it to.

#Where can I get cVim?

 * There are two ways:
  * You can install it through the [Chrome web store](https://chrome.google.com/webstore/detail/cvim/ihlenndgcmojhcghmfjfneahoeklbjjh)
  * You can download the `.zip` file [here](https://github.com/1995eaton/chromium-vim/archive/master.zip) and enable cVim by going to the `chrome://extensions` URL and checking developer mode, then pointing Chrome to the unzipped folder via the `Load unpacked extensions...` button.

# Why is this different than Vimium, ViChrome, or Vrome?

These extensions do a wonderful job of adding Vim-like keybindings to Google Chrome, but they lack many of the features that Firefox Addon, Pentadactyl, have.

 * What features does cVim add to Chrome?
  * Google/IMDB/Wikipedia/Amazon/Duckduckgo/Yahoo/Bing search completion
  * Support for custom search engines
  * History and Bookmark search/completion with bookmark folder support
  * Caret/Visual mode
  * Efficient link hints (with support for custom mappings)
  * Support for custom keyboard mappings
  * Regex page search with highlighting
  * Command bar with tab-completion
  * Smooth scrolling

#cVim Help
###cVimrc

 * Boolean cVimrc settings are enabled with the command ```'set' + <SETTING_NAME>``` and disabled with
   the command ```'set' + no<SETTING_NAME>``` (for example, ```set regexp``` and ```set noregexp```)
 * Boolean cVimrc settings can be inversed by adding "!" to the end
 * Other settings are defined with ```=``` used as a separator and are prefixed by ```let``` (for example, ```let hintcharacters="abc"```)

| setting                             | type                               | description                                                                               | default                                                                     |
| ----------------------------------- | ---------------------------------- | ----------------------------------------------------------------------------------------- | --------------------------------------------------------------------------: |
| searchlimit                         | integer                            | set the amount of results displayed in the command bar                                    | 20                                                                          |
| scrollstep                          | integer                            | set the amount of pixels scrolled when using the scrollUp and scrollDown commands         | 75                                                                          |
| timeoutlen                          | integer                            | The amount of time to wait for a `<Leader>` mapping in milliseconds                       | 1000                                                                        |
| fullpagescrollpercent               | integer                            | set the percent of the page to be scrolled by when using the scrollFullPageUp and scrollFullPageDown commands | 85                                                      |
| typelinkhintsdelay                  | integer                            | the amount of time (in milliseconds) to wait before taking input after opening a link hint with typelinkhints and numerichints enabled | 500                            |
| scrollduration                      | integer                            | the duration of smooth scrolling                                                          | 20                                                                          |
| hud                                 | boolean                            | show the heads-up-display                                                                 | true                                                                        |
| regexp                              | boolean                            | use regexp in find mode                                                                   | true                                                                        |
| ignorecase                          | boolean                            | ignore search case in find mode                                                           | true                                                                        |
| linkanimations                      | boolean                            | show fade effect when link hints open and close                                           | false                                                                       |
| numerichints                        | boolean                            | use numbers for link hints instead of a set of characters                                 | false                                                                       |
| dimhintcharacters                   | boolean                            | dim letter matches in hint characters rather than remove them from the hint               | true                                                                        |
| defaultnewtabpage                   | boolean                            | use the default chrome://newtab page instead of a blank page                              | false                                                                       |
| cncpcompletion                      | boolean                            | use <C-n> and <C-p> to cycle through completion results (requires you to set the nextCompletionResult keybinding in the chrome://extensions page (bottom right) | false |
| smartcase                           | boolean                            | case-insensitive find mode searches except when input contains a capital letter           | true                                                                        |
| incsearch                           | boolean                            | begin auto-highlighting find mode matches when input length is greater thant two characters | true                                                                      |
| typelinkhints                       | boolean                            | (numerichints required) type text in the link to narrow down numeric hints                | false                                                                       |
| autohidecursor                      | boolean                            | hide the mouse cursor when scrolling (useful for Linux, which doesn't auto-hide the cursor on keydown) | false |
| autofocus                           | boolean                            | allows websites to automatically focus an input box when they are first loaded            | true                                                                        |
| insertmappings                      | boolean                            | use insert mappings to navigate the cursor in text boxes (see bindings below)             | true                                                                        |
| smoothscroll                        | boolean                            | use smooth scrolling                                                                      | true                                                                        |
| completionengines                   | array of strings                   | use only the specified search engines                                                     | []                                                                          |
| blacklists                          | array of strings                   | disable cVim on the sites matching one of the patterns                                    | []                                                                          |
| mapleader                           | string                             | The default `<Leader>` key                                                                | \                                                                           |
| highlight                           | string                             | the highlight color in find mode                                                          | "#ffff00"                                                                   |
| defaultengine                       | string                             | set the default search engine                                                             | "google"                                                                    |
| locale                              | string                             | set the locale of the site being completed/searched on (see example configuration below)  | ""                                                                          |
| activehighlight                     | string                             | the highlight color for the current find match                                            | "#ff9632"                                                                   |
| homedirectory                       | string                             | the directory to replace `~` when using the `file` command                                | ""                                                                          |
| qmark &lt;alphanumeric charcter&gt; | string                             | add a persistent QuickMark (e.g. ```let qmark a = ["http://google.com", "http://reddit.com"]```) | none                                                                 |
| previousmatchpattern                | string (regexp)                    | the pattern looked for when navigating a page's back button                               | ((?!last)(prev(ious)?&#124;back&#124;«&#124;less&#124;&lt;&#124;‹&#124; )+) |
| nextmatchpattern                    | string (regexp)                    | the pattern looked for when navigation a page's next button                               | ((?!first)(next&#124;more&#124;&gt;&#124;›&#124;»&#124;forward&#124; )+)    |
| hintcharacters                      | string (alphanumeric)              | set the default characters to be used in link hint mode                                   | "asdfgqwertzxcvb"                                                           |
| barposition                         | string &lt;br&gt;["top", "bottom"] | set the default position of the command bar                                               | "top"                                                                       |

###Example configuration
```viml
" Settings
set nohud
set nosmoothscroll
set noautofocus "The opposite of autofocus; this setting stops sites from focusing on an input box when they load
set typelinkhints
let searchlimit = 30
let scrollstep = 70
let barposition = "bottom"
let locale = "uk" "Current choices are 'jp' and 'uk'. This allows cVim to use sites like google.co.uk or google.co.jp to search rather than google.com. Support is currently very limited. Let me know if you need a different locale for one of the completion/search engines
let hintcharacters = "abc123"
let searchengine dogpile = "http://www.dogpile.com/search/web?q=%s" "If you leave out the '%s' at the end of the URL, your query will be appended to the link. Otherwise, your query will replace the '%s'.
let completionengines = ["google", "amazon", "imdb", "dogpile"]
let searchalias g = "google" "Create a shortcut for search engines. For example, typing ':tabnew g example' would act the same way as ':tabnew google example'
let qmark a = ["http://www.reddit.com", "http://www.google.com", "http://twitter.com"]  "Open all of these in a tab with `gnb` or open one of these with <N>goa where <N>
let blacklists = ["https://mail.google.com/*", "*://*.reddit.com/*"]
let mapleader = ","

" Mappings

map <Leader>r reloadTabUncached
map <Leader>x :restore<Space>

map j scrollUp "This remaps the default 'j' mapping
map gb :buffer<Space> "You can use <Space>, which is interpreted as a literal " " character, to enter buffer completion mode
unmap k "The unmaps the default 'k' mapping

map f F "This remaps the default 'f' mapping to the current 'F' mapping

map <C-h> :set hud!<CR> "Toggle the current HUD display value
map <C-i> :set numerichints!<CR> "Switch between alphabetical hint characters and numeric hints
map <C-u> rootFrame
map <M-h> previousTab
map <C-d> scrollPageDown
map <C-e> scrollPageUp
iunmap <C-y>
imap <C-m> deleteWord
map X :execute gTx<CR> "Close the current tab and move to the one before it
```

###Blacklists
 * You can blacklist specific commands on chosen domains by adding the keybinding after the blacklist URL. For instance, if you want smooth scrolling enabled with the &lt;Up&gt; and &lt;Down&gt; keys, but not on pages like Chrome's built-in PDF viewer (in which the up and down keys won't respond if they have been mapped), your cVimrc would look like this:
```viml
map <Up> scrollUp
map <Down> scrollDown
```
and the blacklists setting would have look like this:
```viml
let blacklists = ["*://*/*.pdf <Up> <Down>"]
```
 * The blacklists setting uses a custom inplementation of Chrome's @match pattern guidelines. See https://developer.chrome.com/extensions/match_patterns for a description of the syntax.

###Mappings
 * Normal mappings are defined with the following structure: ```map <KEY> <MAPPING_NAME>```
 * Insert mappings use the same structure, but use the command "imap" instead of "map"
 * Control, meta, and alt can be used also:
```viml
<C-u> "Ctrl + u
<M-u> "Meta + u
<A-u> "Alt  + u
```
 * It is also possible to unmap default bindings with ```unmap <KEY>``` and insert bindings with ```iunmap <KEY>```
 * To unmap all default keybindings, use ```unmapAll```. To unmap all default insert bindings, use ```iunmapAll```

###Tabs
 * Commands that open links (`:tabnew` and `:open`) have three different properties
  * `!` => Open in a new tab
  * `&` => Open in a new tab (inactive/unfocused)
  * `*` => Pin the tab
 * The use of these properties are best explained with examples:

```viml
:open! google<CR> "This is the same as :tabnew google<CR>
:open google!<CR> "This is another way of writing the above (these flags can can be added to either the base command or the end of the final command)

:open& google<CR> "This will open Google in a new inactive tab

:open&* google<CR> "The will open Google in a new inactive, pinned tab
:tabnew google&*<CR> "Once again, this will do the same thing as the above command
:open google&*<CR> "Again, same as above

:open google!& "Here, the & flag will cancel out the ! flag, opening Google in a new inactive tab

"More examples
:bookmarks my_bookmark.com& "inactive,new tab
:bookmarks&* my_bookmark.com "inactive,pinned,new tab
:bookmarks! my_bookmark.com "new tab
:bookmarks my_bookmark.com "same tab
```


#Keybindings

| Movement                  |                                                                       | Mapping name                    |
| ------------------------- | :-------------------------------------------------------------------- | :------------------------------ |
| j, s                      | scroll down                                                           | scrollDown                      |
| k, w                      | scroll up                                                             | scrollUp                        |
| h                         | scroll left                                                           | scrollLeft                      |
| l                         | scroll right                                                          | scrollRight                     |
| d                         | scroll half-page down                                                 | scrollPageDown                  |
| unmapped                  | scroll full-page down                                                 | scrollFullPageDown              |
| u, e                      | scroll half-page up                                                   | scrollPageUp                    |
| unmapped                  | scroll full-page up                                                   | scrollFullPageUp                |
| gg                        | scroll top the top of the page                                        | scrollToTop                     |
| G                         | scroll to the bottom of the page                                      | scrollToBottom                  |
| 0                         | scroll to the left of the page                                        | scrollToLeft                    |
| $                         | scroll to the right of the page                                       | scrollToRight                   |
| gi                        | go to first input box                                                 | goToInput                       |
| gI                        | go to the last focused input box by `gi`                              | goToLastInput                   |
| zz                        | center page to current search match (middle)                          | centerMatchH                    |
| zt                        | center page to current search match (top)                             | centerMatchT                    |
| zb                        | center page to current search match (bottom)                          | centerMatchB                    |
| **Link Hints**            |                                                                       |                                 |
| f                         | open link in current tab                                              | createHint                      |
| F                         | open link in new tab                                                  | createTabbedHint                |
| unmapped                  | open link in new tab (active)                                         | createActiveTabbedHint          |
| W                         | open link in new window                                               | createHintWindow                |
| A                         | repeat last hint command                                              | openLastHint                    |
| q                         | trigger a hover event (mouseover + mouseenter)                        | createHoverHint                 |
| Q                         | trigger a unhover event (mouseout + mouseleave)                       | createUnhoverHint               |
| mf                        | open multiple links                                                   | createMultiHint                 |
| mr                        | reverse image search multiple links                                   | multiReverseImage               |
| my                        | yank multiple links (open the list of links with P)                   | multiYankUrl                    |
| gy                        | copy url from link to clipboard                                       | yankUrl                         |
| gr                        | reverse image search (google images)                                  | reverseImage                    |
| ;                         | change the link hint focus                                            |                                 |
| **QuickMarks**            |                                                                       |                                 |
| M&lt;*&gt;                | create quickmark &lt;*&gt;                                            | addQuickMark                    |
| go&lt;*&gt;               | open quickmark &lt;*&gt; in the current tab                           | openQuickMark                   |
| &lt;N&gt;gn&gt;           | open quickmark &lt;*&gt; in a new tab &lt;N&gt; times                 | openQuickMarkTabbed             |
| **Miscellaneous**         |                                                                       |                                 |
| a                         | alias to ":tabnew google "                                            | :tabnew google                  |
| :                         | open command bar                                                      | openCommandBar                  |
| &lt;A-z&gt;               | toggle cVim (same as disable cVim option in toolbar icon)             | toggleCvim                      |
| unmapped                  | toggle the blacklist on the current domain                            | toggleBlacklisted               |
| /                         | open search bar                                                       | openSearchBar                   |
| ?                         | open search bar (reverse search)                                      | openSearchBarReverse            |
| I                         | search through browser history                                        | :history                        |
| &lt;N&gt;g%               | scroll &lt;N&gt; percent down the page                                | percentScroll                   |
| zr                        | restart Google Chrome                                                 | :chrome://restart&lt;CR&gt;     |
| i                         | enter insert mode (escape to exit)                                    | insertMode                      |
| r                         | reload the current tab                                                | reloadTab                       |
| gR                        | reload the current tab + local cache                                  | reloadTabUncached               |
| ;&lt;*&gt;                | create mark &lt;*&gt;                                                 | setMark                         |
| ''                        | go to last scroll position                                            | lastScrollPosition              |
| '&lt;*&gt;                | go to mark &lt;*&gt;                                                  | goToMark                        |
| none                      | reload all tabs                                                       | reloadAllTabs                   |
| cr                        | reload all tabs but current                                           | reloadAllButCurrent             |
| zi                        | zoom page in                                                          | zoomPageIn                      |
| zo                        | zoom page out                                                         | zoomPageOut                     |
| z0                        | zoom page to original size                                            | zoomOrig                        |
| z&lt;Enter&gt;            | toggle image zoom (same as clicking the image on image-only pages)    | toggleImageZoom                 |
| gd                        | alias to :chrome://downloads&lt;CR&gt;                                | :chrome://downloads&lt;CR&gt;   |
| yy                        | copy the url of the current page to the clipboard                     | yankDocumentUrl                 |
| b                         | search through bookmarks                                              | :bookmarks                      |
| p                         | open the clipboard selection                                          | openPaste                       |
| P                         | open the clipboard selection in a new tab                             | openPasteTab                    |
| ci                        | toggle visibility of images on the current webpage                    | toggleImages                    |
| gj                        | hide the download shelf                                               | hideDownloadsShelf              |
| gf                        | cycle through iframes                                                 | nextFrame                       |
| gF                        | go to the root frame                                                  | rootFrame                       |
| gq                        | stop the current tab from loading                                     | cancelWebRequest                |
| gQ                        | stop all tabs from loading                                            | cancelAllWebRequests            |
| gu                        | go up one path in the URL                                             | goUpUrl                         |
| gU                        | go to to the base URL                                                 | goToRootUrl                     |
| gs                        | go to the view-source:// page for the current Url                     | goToSource                      |
| **Tab Navigation**        |                                                                       |                                 |
| gt, K, R                  | navigate to the next tab                                              | nextTab                         |
| gT, J, E                  | navigate to the previous tab                                          | previousTab                     |
| g0, g$                    | go to the first/last tab                                              | firstTab, lastTab               |
| &lt;C-S-h&gt;, gh         | open the last URL in the current tab's history in a new tab           | openLastLinkInTab               |
| &lt;C-S-l&gt;, gl         | open the next URL from the current tab's history in a new tab         | openNextLinkInTab               |
| x                         | close the current tab                                                 | quit                            |
| gxT                       | close the tab to the left of the current tab                          | closeTabLeft                    |
| gxt                       | close the tab to the right of the current tab                         | closeTabRight                   |
| gx0                       | close all tabs to the left of the current tab                         | closeTabsToLeft                 |
| gx$                       | close all tabs to the right of the current tab                        | closeTabsToRight                |
| X                         | open the last closed tab                                              | lastClosedTab                   |
| t                         | :tabnew                                                               | :tabnew                         |
| T                         | :tabnew &lt;CURRENT URL&gt;                                           | :tabnew @%                      |
| O                         | :open &lt;CURRENT URL&gt;                                             | :open @%                        |
| &lt;N&gt;%                | switch to tab &lt;N&gt;                                               | goToTab                         |
| H, S                      | go back                                                               | goBack                          |
| L, D                      | go forward                                                            | goForward                       |
| B                         | search for another active tab                                         | :buffer                         |
| &lt;                      | move current tab left                                                 | moveTabLeft                     |
| &gt;                      | move current tab right                                                | moveTabRight                    |
| ]]                        | click the "next" link on the page (see nextmatchpattern above)        | nextMatchPattern                |
| [[                        | click the "back" link on the page (see previousmatchpattern above)    | previousMatchPattern            |
| gp                        | pin/unpin the current tab                                             | pinTab                          |
| **Find Mode**             |                                                                       |                                 |
| n                         | next search result                                                    | nextSearchResult                |
| N                         | previous search result                                                | previousSearchResult            |
| v                         | enter visual/caret mode (highlight current search/selection)          | toggleVisualMode                |
| V                         | enter visual line mode from caret mode/currently highlighted search   | toggleVisualLineMode            |
| **Visual/Caret Mode**     |                                                                       |                                 |
| escape                    | exit visual mode to caret mode/exit caret mode to normal mode         |                                 |
| v                         | toggle between visual/caret mode                                      |                                 |
| h, j, k, l                | move the caret position/extend the visual selection                   |                                 |
| y                         | copys the current selection                                           |                                 |
| n                         | select the next search result                                         |                                 |
| N                         | select the previous search result                                     |                                 |
| p                         | open highlighted text in current tab                                  |                                 |
| P                         | open highlighted text in new tab                                      |                                 |
| **Text boxes**            |                                                                       |                                 |
| &lt;C-i&gt;               | move cursor to the beginning of the line                              | beginningOfLine                 |
| &lt;C-e&gt;               | move cursor to the end of the line                                    | endOfLine                       |
| &lt;C-u&gt;               | delete to the beginning of the line                                   | deleteToBeginning               |
| &lt;C-o&gt;               | delete to the end of the line                                         | deleteToEnd                     |
| &lt;C-y&gt;               | delete back one word                                                  | deleteWord                      |
| &lt;C-p&gt;               | delete forward one word                                               | deleteForwardWord               |
| &lt;C-h&gt;               | move cursor back one word                                             | backwardWord                    |
| &lt;C-l&gt;               | move cursor forward one word                                          | forwardWord                     |
| &lt;C-f&gt;               | move cursor forward one letter                                        | forwardChar                     |
| &lt;C-b&gt;               | move cursor back one letter                                           | backwardChar                    |

#Command Mode

| Command                                     | Description                                                                            |
| ------------------------------------------- | -------------------------------------------------------------------------------------- |
| :tabnew (autocomplete)                      | open a new tab with the typed/completed search                                         |
| :new (autocomplete)                         | open a new window with the typed/completed search                                      |
| :open (autocomplete)                        | open the typed/completed url/google search                                             |
| :history (autocomplete)                     | search through browser history                                                         |
| :bookmarks (autocomplete)                   | search through bookmarks                                                               |
| :bookmarks /&lt;folder&gt; (autocomplete)   | browse bookmarks by folder/open all bookmarks from folder                              |
| :set (autocomplete)                         | temporarily change a cVim setting                                                      |
| :chrome:// (autocomplete)                   | open a chrome:// url                                                                   |
| :tabhistory (autocomplete)                  | browse the different history states of the current tab                                 |
| :quit                                       | close the current tab                                                                  |
| :date                                       | display the current date                                                               |
| :restore (autocomplete)                     | restore a previously closed tab (newer versions of Chrome only)                        |
| :tabattach (autocomplete)                   | move the current tab to another open window                                            |
| :file (autocomplete) [expirimental]         | open a local file                                                                      |
| :duplicate                                  | duplicate the current tab                                                              |
| :settings                                   | open the settings page                                                                 |
| :nohl                                       | clear the highlighted text from the last search                                        |
| :execute                                    | execute a sequence of keys (Useful for mappings. For example, "map j :execute 2j<CR>") |
| :buffer (autocomplete)                      | change to a different tab                                                              |
| :mksession                                  | create a new session from the current tabs in the active window                        |
| :delsession (autocomplete)                  | delete a saved session                                                                 |
| :session (autocomplete)                     | open the tabs from a saved session in a new window                                     |

#Tips

 * You can use @% in "open" commands to specify the current URL. For example, ":open @%" would essentially refresh the current page.
 * Prepend a number to the command to repeat that command N times
 * Use the up/down arrows in command/find mode to navigate through previously executed commands/searches -- you can also use this to search for previously executed commands starting with a certain combination of letters (for example, entering "ta" in the command bar and pressing the up arrow will search command history for all matches beginning with "ta"

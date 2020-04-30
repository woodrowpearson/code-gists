# AppleScript

```text
-- Scrape all URLs from all tabs in all windows
-- https://forum.keyboardmaestro.com/t/save-and-restore-safari-session-tabs/15036/4
set AppleScript's text item delimiters to linefeed
tell application "Safari"
   set urlList to (URL of tabs of windows) as text
end tell
return urlList
```

```text
-- Expand Typinator abbreviation
tell application "Typinator"
  expand string "dd"
end tell
```

```text
-- Print URL of current tab
tell app "safari" to url of document 1
```

```text
-- Show source of current document
tell app "safari" to source of document 1
```

```text
-- Activate menu bar of an app

-- Accepts a list of form: `{"Finder", "View", "Arrange By", "Date"}`
-- Execute the specified menu item.  In this case, assuming the Finder
-- is the active application, arranging the frontmost folder by date.
on menu_click(mList)
  local appName, topMenu, r

  -- Validate our input
  if mList's length < 3 then error "Menu list is not long enough"

  -- Set these variables for clarity and brevity later on
  set {appName, topMenu} to (items 1 through 2 of mList)
  set r to (items 3 through (mList's length) of mList)

  -- This overly-long line calls the menu_recurse function with
  -- two arguments: r, and a reference to the top-level menu
  tell application "System Events" to my menu_click_recurse(r, ((process appName)'s ¬
    (menu bar 1)'s (menu bar item topMenu)'s (menu topMenu)))
end menu_click

on menu_click_recurse(mList, parentObject)
  local f, r

  -- `f` = first item, `r` = rest of items
  set f to item 1 of mList
  if mList's length > 1 then set r to (items 2 through (mList's length) of mList)

  -- Either actually click the menu item, or recurse again
  tell application "System Events"
    if mList's length is 1 then
      click parentObject's menu item f
    else
      my menu_click_recurse(r, (parentObject's (menu item f)'s (menu f)))
    end if
  end tell
end menu_click_recurse

-- Example of use
tell application "Safari" to activate

menu_click({"Safari", "Bookmarks", "Edit Bookmarks"})
```

```text
-- Get path of app
POSIX path of (path to application "Sublime Text")
```

```text
-- Assign variable to system variable
set var1 to (system attribute "var1")
```

```text
-- Trigger a keypress
-- http://macbiblioblog.blogspot.com/2014/12/key-codes-for-function-and-special-keys.html

-- Trigger caps lock and tilda together
tell application "System Events" to key code 50 using {option down, control down}

-- Trigger ⌘ + a
tell application "System Events" to keystroke "a" using command down

-- Trigger ⏎
tell application "System Events" to key code 36
```

```text
-- Run KM macro
tell application "Keyboard Maestro Engine"
do script "w: github"
end tell
```

```text
-- Capture first argument to script

-- Need to wrap it in run argv clause
on run argv
  tell application "System Events"
    -- Type out the first argument
    keystroke (item 1 of argv)
  end tell
end run
```

```text
-- Type something
tell application "System Events"
  keystroke "Hello"
end tell
```

```text
-- Get path of open document in an app

-- Change "MacDown" to another app
tell application "MacDown" to set file_path to file of front document
```

```text
-- Get URL of open Safari tab
tell application "Safari" to return URL of front document
```

```text
-- Convert to POSIX path
set inputPath to POSIX path of input
```

```text
-- Select first result from google search and load it in the front tab.
-- Works on Safari only.

set xpathStr to "//*[@class=\\'r\\']/a"
set strJS to "

var xpathResults = document.evaluate('" & xpathStr & "', document, null, 0, null),
  nodeList = [],
  oNode;

while (oNode = xpathResults.iterateNext()) {
  nodeList.push(oNode.href);
}

nodeList;

"
tell application "Safari"
  set linkList to (do JavaScript strJS in front document)

  if linkList ≠ {} then
    set firstLink to item 1 of linkList
    set URL of front document to firstLink
  end if

end tell
```

```text
-- Search Alfred with query
osascript -e "tell application \"Alfred 4\" to search \"$*\""
```

```text
-- Get number of Safari windows
tell application "Safari"
   set numberOfSafariWindows to length of (get current tab of windows)
end tell
```

```text
-- Search for tag in finder
on run argv
  set theQuery to first item of argv

  tell application "Finder"
    make new Finder window
    activate
  end tell
  delay 0.2
  tell application "System Events" to tell process "Finder"
    keystroke "f" using command down
    delay 0.1
    keystroke "tag:"
    keystroke theQuery
    key code 36  -- Return
  end tell
end run
```

```text
-- Check if currently running app is full screen
tell application "System Events"
    tell (first application process whose frontmost is true)
      tell (first window whose subrole is "AXStandardWindow")

        value of attribute "AXFullScreen"
      end tell
    end tell
  end tell
```

```text
-- Set front window of front app to full-screen
try
  tell application "System Events"
    tell (first application process whose frontmost is true)
      tell (first window whose subrole is "AXStandardWindow")

        set fullScreen to value of attribute "AXFullScreen"

        if fullScreen = false then
          set value of attribute "AXFullScreen" to true
        end if

      end tell
    end tell
  end tell

on error e number n
  set e to e & return & return & "Num: " & n
  if n ≠ -128 then
    try
      tell application (path to frontmost application as text) to set ddButton to button returned of ¬
        (display dialog e with title "ERROR!" buttons {"Copy Error Message", "Cancel", "OK"} ¬
          default button "OK" giving up after 30)
      if ddButton = "Copy Error Message" then set the clipboard to e
    end try
  end if
end try
```

```text
-- Set clipboard to
set the clipboard to "Some text"
```

```text
-- cd to passed in dir in iTerm
on run argv
  set theQuery to item 1 of argv
  set cmdStr to "cd " & theQuery
  tell application "iTerm"
    if exists window 1 then
      tell current window
        tell current session to write text cmdStr
      end tell
    else
      create window with default profile
      tell current window
        tell current session to write text cmdStr
      end tell
    end if
  end tell
end run
```

```text
-- Run shell command in sudo mode
do shell script "command here" with administrator privileges
```


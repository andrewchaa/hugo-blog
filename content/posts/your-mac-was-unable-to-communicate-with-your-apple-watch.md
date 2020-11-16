---
title: "Your Mac was unable to communicate with your Apple Watch"
date: 2020-11-15T19:45:09Z
draft: false
---
# Your Mac was unable to communicate with your Apple Watch

I've had this issue since I changed my phone to iPhone 12. I had to reset the apple watch to pair with the new iPhone and after that, lost the convenience to unlock my MacBook with the watch. It was a little sweet luxury to unlock my machine without paying too much attention. I sound like an Apple fanboy and turn out to be. I blame all this to the old iPhone 3GS. Until I had it, I was just an ordinary Windows boy at home and at work.

Btw, to fix the issue, you have to

* Clean all Auto Unlock in your key chain
* Delete a couple of Auto Unlock files in the file system

The below is the tip from an answer from apple discussion [https://discussions.apple.com/thread/251826134](https://discussions.apple.com/thread/251826134)

> Steps \(follow at your own discretion\)
>
> 1. Open "Keychain Access"
> 2. In "View", enable "Show Invisible Items"
> 3. Search for "Auto Unlock"
> 4. You should see a whole bunch of application passwords for "Auto Unlock: XXXX's ..."
> 5. Select all records and delete \(this will reset/disable auto unlock on other Macs if you use multiple Macs\)
> 6. Whilst still in "Keychain Access", search for "AutoUnlock" \(no space\)
> 7. There should be 4 entries for "tlk" "tlk-nonsync" "classA" "classC"
> 8. Select 4 records and delete \(don't worry if they re-appear, the system repairs this automatically\)
> 9. Open "Finder" and navigate to "~/Library/Sharing/AutoUnlock"
> 10. There should be two files "ltk.plist" and "pairing-records.plist"
> 11. Delete both files
> 12. Open "System Preferences" and try enabling auto unlock. You may need to enable it twice, the first attempt will fail.


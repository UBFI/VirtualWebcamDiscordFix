# VirtualWebcamDiscordFix
Bring back virtual webcam support to discord for MacOS on M1


To provide a bit of context as to why this is relevant since the M1 released a new type of sandboxing has been implemented this does not allow for a virtual webcam to communicate with userland apps that exist within a sandbox such as Discord. The sandbox attribute is part of the applications entitlment and under normal circumstances can't be change. Most people suggest removing the signature all together but on M1 this will keep it from running. I targeted which applications needs this flag disabled and posted the commands I use on my M1 canary build of discord. Canary by default is a hybrid native/intel application so it will run on M1 metal.

```
codesign --force --deep --sign - /Applications/Discord\ Canary.app/Contents/Frameworks/Discord\ Canary\ Helper\ \(GPU\).app
codesign --force --deep --sign - /Applications/Discord\ Canary.app/Contents/Frameworks/Discord\ Canary\ Helper.app 
codesign --force --deep --sign - /Applications/Discord\ Canary.app/Contents/Frameworks/Discord\ Canary\ Helper\ \(Plugin\).app
codesign --force --deep --sign - /Applications/Discord\ Canary.app/Contents/Frameworks/Discord\ Canary\ Helper\ \(Renderer\).app 
```
The above commands will resign each app bundle without any entitlments disabling the sandbox attribute and allowing you to use a virtual webcam once again. You can also lock the Resources and Framewords directory in the main app bundle to keep updates from breaking your changes or removing your better discord shim.
UPDATE: All branches now support M1. Below is the command block for discords notmal release branch, just click copy and paste in terminal.
```
codesign --force --deep --sign - /Applications/Discord.app/Contents/Frameworks/Discord\ Helper\ \(GPU\).app
codesign --force --deep --sign - /Applications/Discord.app/Contents/Frameworks/Discord\ Helper.app 
codesign --force --deep --sign - /Applications/Discord.app/Contents/Frameworks/Discord\ Helper\ \(Plugin\).app
codesign --force --deep --sign - /Applications/Discord.app/Contents/Frameworks/Discord\ Helper\ \(Renderer\).app 
```

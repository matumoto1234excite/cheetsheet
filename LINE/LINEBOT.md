# LINEBOT

ここにすべてが書いてある。神。

https://qiita.com/shinbunbun_/items/7efef6db31514831143d





打ったコマンド一覧

```bash
$ git clone https://github.com/shinbunbun/aizuhack-bot.git
$ cd aizuhack-bot/
$ npm i
$ npx vercel login
> githubでログインした
$ npx vercel link
> Set up “~/code_box/code_box_sub/AizuHack/line_course/aizuhack-bot”? [Y/n] y
> Which scope should contain your project? matumoto1234
> Link to existing project? [y/N] n
> What’s your project’s name? aizuhack-bot
> In which directory is your code located? ./
> No framework detected. Default Project Settings:
ここでなにやったか覚えてない
> Want to override the settings? [y/N] n
$ npx vercel env add
> What’s the name of the variable? channelAccessToken
> What’s the value of channelAccessToken? /seuhitdSQCGbiTc7IVnDtfi9bwRZmVMFAYqNdjO8QiVrIv/f+3k
CeKfwoJxrxCUbh4SRhXSQ4wN3RN/u+ClRWAWuLwq+K0NYbrlnJf6KRCgpAydD4ZYfsTSZFImmF6pjzrhnezyJXtzTYBRtV
sUuwdB04t89/1O/w1cDnyilFU=
> Add channelAccessToken to which Environments (select multiple)? Production, Preview, Develop
ment
$ npx vercel env add
> What’s the name of the variable? channelSecret
> What’s the value of channelSecret? 98316dffa2457c6a9013ca81447587f6
> Add channelSecret to which Environments (select multiple)? Production, Preview, Development
$ npx vercel deploy
🔍  Inspect: https://vercel.com/matumoto1234/aizuhack-bot/4y6TB7SLPCY8pDD5mpb3UrNWswgJ [3s]
✅  Production: https://aizuhack-bot-nine.vercel.app [37s]
📝  Deployed to production. Run `vercel --prod` to overwrite later (https://vercel.link/2F).
💡  To change the domain or build command, go to https://vercel.com/matumoto1234/aizuhack-bot/settings
```


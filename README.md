# Best practices for Discord bots


*NB: These guidelines are intended for bots running on public servers. If your
bot is restricted to private ones, this document likely doesn't apply to you.*

1. #### Command Prefixes
   1. **Commands should be explicitly invoked**  
      Bots should not activate on normal chat. Instead, use a command prefix or only respond when your bot is directly @mentioned.
   2. **Use unique prefixes**  
      Single-character prefixes such as `!`, `$` and `.` are commonplace for activating commands and lead to overlaps with other bots.  
      Should you opt to use a prefix for your bot, consider using words (`owl`) or unique Unicode characters (`¨`). Also, you should avoid using `#` or `@` as prefixes since they can be used to mention a channel or a member.  
      Ideally, your bot's prefix should be configurable on a server-by-server basis, so that the server owners can ensure every bot has its own unique prefix of their choice.
   3. **Don't be greedy**  
      Restrict yourself to a small number of prefixes to reduce the risk of collision with others.
   4. **Don't overuse mentions**  
      If you reply directly to a command, don't use a mention, they can lead to bot reply loops. Mentions are fine if a long-running command is executed, but private messages are a good alternative. Alternatively can you add a Zero-width-space (`\u200E`) before the mention to prevent other bots from triggering.

2. #### Commands
   1. **Have an `info` command**  
      It should provide information about the bot such as what framework it is using and the used version, `help` commands and, most importantly, who made it.
   2. **Don't reply with "invalid command"**  
      If a user uses a command that does not exist, then let it fail silently. Do not have it reply with something like "invalid command".  
      Though if the command is correct, but arguments are wrong then it's okay to reply with "invalid args". If there is more than one bot in a server that shares a prefix, this can result in very obnoxious usage.
   3. **Only ask for and use permissions the bot and user need**  
      Having a Mute-command require the `Manage Guild` permission for the command executor doesn't make sense.  
      If a command should be restricted by permissions should they make sense. This also counts for Bots which ask for and even require Administrator permissions to function.  
      A bot should NEVER rely on Administrator! [Read more about why here](https://www.andre601.ch/blog/posts/2021/09-28-bots-and-admin/).

3. #### API and behaviour
   1. **Be respectful of Discord's API**  
      Bots that abuse and misuse the Discord API ruin things for everyone.  
      Make sure to factor in rate-limiting and backoff in your bot code, and be intelligent about using the API. Make sure to ask for help if you're unsure about the right way to implement things.
   2. **Ignore both your own and other bots' messages**  
      This helps prevent infinite self-loops and potential security exploits.  
      Using a zero width space such as `\u200B` and `\u180E` in the beginning of each message also prevents your bot from triggering other bots' commands.  
      The Discord API also tells you if a user is a bot (`bot` property on `User` objects - [see the reference](https://discord.com/developers/docs/resources/user#user-object)).
   3. **Keep NSFW features locked to NSFW channels**  
      All NSFW commands/features should only work in (Discord) NSFW-marked channels.
   4. **Use mentioning the bot to help users.**  
      Allowing a mention as the prefix ("@MyBot help") or adding a way to find the bot's prefix with only a mention ("@MyBot" or "@MyBot, what's your prefix?") will help users who are new to your bot in getting started (Make sure that whatever the message is, it's easily found. A great way to do this is by including it in your bot's presence).  
      The alternative is brute-forcing punctuation characters to find it, which will be difficult for bots following 2 and 3. Plus, a mention is the most unique prefix of all.

4. #### Privacy Policy
   1. **You must have a privacy policy for your bot**
      Discord now expects bot owners to have a privacy policy for your bot, and so does some bot listing services such as Discord Extreme List, and is adapted from what a Discord Staff have generally outlined as required. Will the following cover every legal obligation you may or may not have as a software developer working with user information? \[We can't speak to this, contact a lawyer if you are concerned\]. Will this cover the basic expectations Discord and most bot lists have set out as a user of Discord's API? Yes.
   2. **You must include the following information in your privacy policy**
      1. What data do you collect, including but not limited to personally identifiable information (PII)?
      2. Why do you need the data?
      3. How do you use the data?
      4. Other than Discord (the company) and the users of your bot on Discord (the platform), who do you share your collected data with, if anyone?
      5. How can users contact you if they have concerns about your bot and/or the privacy policy?
      6. If you store data, how can users request it, ask for it to be corrected, or have it removed?
   3. **If you don't collect data, you still need a privacy policy**
      If you don't collect any data from users, you still need to provide a privacy policy. This privacy policy can simply just say "We don't store any user information or data" and how users can contact you if they have any concerns about your bot and/or the privacy policy.
   4. **Your privacy policy can be anywhere accessible (i.e., website, in a bot command, or on a GitHub Gist)**
      As long as your privacy policy is easily accessible and meets all of the above criteria, you can host your privacy policy anywhere. For example, you could have it as a command on your Discord bot, on your bot website, on a GitHub Gist.

If you have an idea for an addition or change to this document, please make a
pull request and we can discuss it.

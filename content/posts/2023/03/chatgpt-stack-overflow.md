---
title: "Will ChatGPT Replace Stack Overflow?"
date: 2023-03-23 07:03:00
tags: [ AI ]
---
**TL&DR:** No. You can move on.

[NANOG87 summary](https://dataplane.org/jtk/blog/2023/02/nanog87/) by John Kristoff prompted me to look at [NANOG87 presentations](https://www.nanog.org/events/nanog-87/agenda/), and one of them discussed [ChatGPT and Network Engineering](https://storage.googleapis.com/site-media-prod/meetings/NANOG87/4699/20230214_Starr_Chatgpt_And_Networking_v1.pdf) ([video](https://youtu.be/stzPJspkUUs)). I couldn't resist the clickbait ;)

Like most _using ChatGPT for something_ articles we're seeing these days, the presentation is a bit too positive for my taste. After all, it's all fine and dandy to claim ChatGPT generates working router configurations and related Jinja2 templates *if you know what the correct configurations should look like and can confidently say "and this is where it made a mistake" afterwards.*
<!--more-->
Could someone who does not know the technology or device configuration details use ChatGPT to create a device configuration? Of course they could, but I wouldn't[^ACL]. It's even worse than pasting random configurations found in blog posts[^RC] or StackOverflow into your production gear.

[^RC]: See also: the road to ~~hell~~ complex designs is [paved with best practices](https://blog.ipspace.net/2011/08/road-to-complex-designs-is-paved-with.html).

Could you use it to generate configurations for a box you never worked with before? Please do, you might greatly improve your troubleshooting skills ;)

[^ACL]: Someone published an ACL generated by ChatGPT that had **permit ip any any** at the top of the ACL. While the rest of the ACL was correct, order of commands does matter sometimes ;)

Anyway, after claiming that...

> ChatGPT is aware of vendor specific syntax and can generate configurations

... which is technically true unless you claim it can generate _working_ or _correct_ configurations, the presentation moved on to solving troubleshooting issues based on Reddit questions, resulting in:

> ChatGPT can potentially help with simple routing troubleshooting, but not with this problem.

Fair enough. On the next question (STP between Juniper and Fortinet) the conclusion was:

> ChatGPT understands STP better than many networking professionals I’ve interviewed over the years.

Let's focus on the _understand_ part of the conclusion. While Sabine Hossenfelder recently argued that [chatbots partly understand what they chat about](https://backreaction.blogspot.com/2023/03/i-believe-chatbots-partly-understand.html) that turned out to be another clickbait -- the way I _understood_ her video, she was effectively saying "we don't have a good definition of what _understand_ means, so whatever." In the ChatGPT-versus-STP case, I'd say the correct conclusion would be:

> ChatGPT can process more source materials and has better regurgitating skills than many networking professionals.

Unfortunately, the _ChatGPT understands STP_ conclusion lead the authors to a follow-up conclusion:

> ChatGPT might result in the obsolescence of many subreddits and Stack Overflow

Well, no. The only reason ChatGPT can make a statement about STP (or any other technology) that sounds about right is because it processed source material talking about those topics. Someone had to generate those materials, and if we assume ChatGPT could generate the results it does from vendor documentation, then it's fair to ask the next question: _do we use Stack Overflow just because we're too lazy to read vendor documentation?_

Sadly, as anyone with decent googling skills who had to turn to Stack Overflow can testify, the reason we're using Stack Overflow as much as we do is because (networking) vendor product documentation focuses on what vendors want you to know: how to configure their product. It often lacks usage guidelines, vendor interoperability, undocumented quirks, gotchas, unintended use cases... not to mention the discussions of how things work. If ChatGPT generates a great answer to a question you'd usually ask on Stack Overflow, it might be because it's processed numerous related answers humans wrote on Stack Overflow ;) Does that make Stack Overflow obsolete? There seems to be a [circular dependency](https://blog.ipspace.net/2021/10/circular-dependencies-considered-harmful.html) somewhere in this paragraph.

Another benefit of finding a "solution" on Stack Overflow[^SO] is voting and feedback, including gems like "_this seems great but it didn't work for me_" or "_while your solution works, that's not how things should be done_." Not exactly something I expect to get from a large language model. After all, the caveats represent a tiny percentage of its training materials.

[^SO]: Anyone forced to use Stack Overflow in a [desperate attempt to solve a rare challenge](https://xkcd.com/979/) knows why I used quotes around the word "solution" ;)

Tim Bray nailed it in [a recent blog post](https://www.tbray.org/ongoing/When/202x/2023/03/14/Binging):

> On the Internet, the truth is paywalled and the bullshit is free. And as just discussed, one of the problems with LLMs is that they’re expensive. Another is that they’re being built by capitalists. Given the choice between expensive quality ingredients and free bullshit, guess which they’ll pick?

Does that make ChatGPT useless? Of course not. I love using it to create introductory paragraphs for my technology resources pages ([example](https://blog.ipspace.net/series/cicd.html)), obviously with full attribution -- it's only fair to tell you it wasn't me drastically improving my writing skills. I would also love to use something like ChatGPT as a friendlier search engine that would understand (here we go again) at least some of my intent[^DB], offer some generic guidelines, and point me to the most appropriate source material. [According to Tim Bray](https://www.tbray.org/ongoing/When/202x/2023/03/14/Binging), Bing's headed in that direction, but it seems like the Bing AI extensions work only with Microsoft Edge (or it's yet again me being too stupid to use it), so whatever.

[^DB]: Sabine Hossenfelder made a great example: it's hard to figure out if dropbox is an English word using a search engine to  -- the results mostly talk about the app. Even 'define:dropbox' trick doesn't work well.
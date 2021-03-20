# 「Computer Security Fundamentals, 4th Edition」の3章
2021/03/21(Sun) 09:00am-10:30am

## 読書会当日に話したいこと

### Chapter 3. Cyber Stalking, Fraud, and Abuse
- [LINEの個人情報、中国の開発委託先から閲覧可能に　「説明不足だった」と謝罪](https://www.itmedia.co.jp/news/articles/2103/17/news127.html)
  - > LINEは国際競争力を確保するため、海外企業に一部の作業を委託して開発スピードを上げているという。当該の中国企業は社内ツールやAI、LINEアプリ内の機能の開発を担っており、LINEは作業に必要な情報として、ユーザーの個人情報にアクセスできるようにしていた。
  - 問題となった理由は「個人情報保護法違反」
    - cf. [個人情報保護委、LINEに報告求める　法的措置も視野：朝日新聞デジタル](https://www.asahi.com/articles/ASP3M6GC4P3MULZU010.html)
    - cf. [管理不備と報じられたLINEの問題についてまとめてみた - piyolog](https://piyolog.hatenadiary.jp/entry/2021/03/19/072110)
- 昨年、これに近いことに遭遇していましたが、みなさんはどうでしたか？
- [アマゾンでマスク詐欺報告相次ぐ　マーケットプレイスで「商品すり替え」「送料50万円」「届かない」など - ITmedia NEWS](https://www.itmedia.co.jp/news/articles/2003/25/news135.html)
  - 当時はどこにいってもマスクがない状況で、半信半疑で注文。
  - 注文後、ちょくちょく発送状況を確認し、配達予定日になっても商品が届かないので問い合わせをし、キャンセルとなる。
  - cf. [Amazon.co.jp: カスタマー Q＆A](https://www.amazon.co.jp/ask/questions/asin/B0851ZKQYM/)

---
## 読書メモ
### Chapter 3. Cyber Stalking, Fraud, and Abuse

```
- Know the various types of Internet investment scams and auction frauds
- Know specific steps to take to avoid fraud on the InternetHave an understanding of what identity theft is and how it is doneKnow specific steps that can be taken to avoid identity theftUnderstand what cyber stalking is and be familiar with relevant lawsKnow how to configure a web browser’s privacy settingsKnow what laws apply to these computer crimes
```

#### Introduction
- > Fraud is one of the most common dangers of the Internet
  - > committing Internet fraud does not require the technical expertise that hacking and virus creation require
  - > a great number of people engaging in various forms of online commerce, and this large amount of business creates a great many opportunities for fraud.

#### cross-site scripting
- > when other users visit that web page, instead of loading a review or comment, their browsers will load the attacker’s script. That script may do any number of things, but it is common for the script to redirect the end user to a phishing website.
- > Cross-site scripting can be `prevented by web developers filtering all user input`. Cross-site scripting will be dealt with in more detail in Chapter 6, “Techniques Used by Hackers.”
  - cf. [動画で知ろう！クロスサイト・スクリプティングの被害！](https://youtu.be/5OF51SNJHxA?t=337)
  - cf. [クロスサイトスクリプティング(XSS)対策としてCookieのHttpOnly属性でどこまで安全になるのか](https://www.youtube.com/watch?v=4JREwhSC2dQ)
  - cf. [『クロスサイトスクリプティング対策』でGoogle検索した上位記事にツッコミを入れる](https://www.youtube.com/watch?v=rEAEUJ1oDjA)

#### Test Your Skills  
- Q1. Candice is discussing Internet fraud with a colleague. She is trying to explain the most common types of fraud. What is the term for the most common type of Internet investment fraud?
  - C. The pump and dumpD. The bait and switch
- Q2. You have become quite active in online investing. You want to get some advice but are concerned about the veracity of the advice you receive. What is the most likely problem with unsolicited investment advice?
  - B. The advice might not be truly unbiased.
- Q3. Juan is a security officer for an investment firm. He is explaining various scams to the brokers. What is the term for artificially inflating a stock in order to sell it at a higher value?
  - C. Pump and dump
- Q4. What is the top rule for avoiding Internet fraud?
  - A. If it seems too good to be true, it probably is.
  - C. Only work with people who have verifiable email addresses.
- Q5. Which of the following is not one of the Security and Exchange Commission’s tips for avoiding investment fraud?
  - B. Consider the source of the offer.
  - C. Always be skeptical.
  - D. Always research the investment.
- Q6. Aliya is active on online auctions but wants to avoid auction fraud. What are the four categories of auction fraud?
  - B. Failure to send, failure to disclose, sending something of lesser value, failure to deliver
- Q7. What is the term for a seller bidding on her own item to drive up the price?
  - C. Shill bidding
- Q8. What is the term for submitting a fake but very high bid to deter other bidders?
  - C. Shill bidding
- Q9. What is typically the goal of identity theft?
  - A. To make illicit purchases
  - D. To invade privacy
- Q10. According to the U.S. Department of Justice, identity theft is generally motivated by what?
  - C. Economic gain
- Q11. Clarence is a police detective with a small-town police department. He is trying to consider how seriously to take reports of cyber stalking. Why is cyber stalking a serious crime?
  - B. It can be a prelude to violent crime.
- Q12. What is cyber stalking?
  - B. Any use of electronic communications to stalk a person
- Q13. What do law enforcement officials usually require of a victim in order to pursue harassment allegations?
  - D. A credible threat of harm
- Q14. If you are posting anonymously in a chat room and another anonymous poster threatens you with assault or even death, is this person’s post harassment?
  - B. Probably not because both parties are anonymous, so the threat is not credible.
    - > Usually law enforcement officials need some credible threat of harm in order to pursue harassment complaints. In simple terms, this means that if you are in an anonymous chat room and someone utters some obscenity, that act probably will not be considered harassment. However, if you receive specific threats via email, those threats would probably be considered harassment.
- Q15. What must exist for cyber stalking to be illegal in a state or territory?
  - A. Specific laws against cyber stalking in that state or territory
- Q16. What is the first step in protecting yourself from identity theft?
  - A. Never provide personal data about yourself unless absolutely necessary.
- Q17. What can you do on your local computer to protect your privacy?
  - A. Install a virus scanner.
  - B. Install a firewall.
  - C. Set your browser’s security settings.
  - D. Set your computer’s filter settings./
- Q18. What is a cookie?
  - A. A piece of data that web servers gather about you
  - B. A small file that contains data and is stored on your computer
- Q19. Which of the following is not an efficient method of protecting yourself from auction fraud?
  - A. Only use auctions for inexpensive items.
- Q20. What is the top rule for chat room safety?
  - B. Never use your real name or any real personally identifying characteristics.
- Q21. Why is it useful to have a separate credit card dedicated to online purchases?
  - D. You can easily cancel that single card if you need to do so.
- Q22. What percentage of cyber stalking cases escalate to real-world violence?
  - D. About 19%
- Q23. If you are a victim of cyber stalking, what should you do to assist the police?
  - C. Keep electronic and hard copies of all harassing communications.
- Q24. What is the top way to protect yourself from cyber stalking?
  - A. Do not use your real identity online.

----
- `auction Fraud`
  - > Internet auction fraud involves schemes attributable to the misrepresentation of a product advertised for sale through an Internet auction site or the non-delivery of products purchased through an Internet auction site. 
    - Source: [Internet Auction Fraud — FBI](https://www.fbi.gov/scams-and-safety/common-scams-and-crimes/internet-auction-fraud)
- `fraud`
  - > Scamは、俗語ですが、お金儲けを目的としたずる賢い計画や行為のことです。
   - > "Fraud"は、"scam"と同じように、お金儲けで誰かを騙す意味もありますが、人間として、実際に持っていない能力などを持っているように見せかけるのも、"fraud"です。
     - Source: [scam (【名詞】詐欺、悪徳商法 ) の意味・使い方・読み方｜DMM英会話Words](https://eikaiwa.dmm.com/app/uknow/word/scam/zga0ELstQmCjlQAAAEAmNw)
- `snake oil`
  - > Snake oil is a euphemism for deceptive marketing, health care fraud, or a scam. Similarly, “snake oil salesman“ is a common expression used to describe someone who deceives people in order to get money from them.
    - Source: [Snake oil - Wikipedia](https://en.wikipedia.org/wiki/Snake_oil)
- `perpetrate`
  - verb
  - meaning: carry out or commit (a harmful, illegal, or immoral action).
    - e.g.: "a crime has been perpetrated against a sovereign state"
- `identity theft`
  - noun
  - meaning: the fraudulent practice of using another person's name and personal information in order to obtain credit, loans, etc.
- `phishing`
  - > フィッシングはphishingという綴りで、魚釣り（fishing）と洗練（sophisticated）から作られた造語である
    - Source: [フィッシング詐欺に注意｜基本的な対策｜一般利用者の対策｜国民のための情報セキュリティサイト](https://www.soumu.go.jp/main_sosiki/joho_tsusin/security/enduser/security01/05.html)
- `purport`
  - verb
  - meaning: appear to be or do something, especially falsely.
    - e.g.: "she is not the person she purports to be"
- `legitimate`
  - adj
  - meaning: according to law; lawful
    - e.g: the property's legitimate owner.
- `sophisticated`
  - adj
  - meaning: (of a machine, system, or technique) developed to a high degree of complexity.
    - e.g.: "highly sophisticated computer systems"
    - Syn: advanced
- `prelude`
  - noun
  - meaning: an action or event serving as an introduction to something more important.
    - e.g.: "a ceasefire had been agreed as a prelude to full peace negotiations"
    - Syn: preliminary, overture, opening
    
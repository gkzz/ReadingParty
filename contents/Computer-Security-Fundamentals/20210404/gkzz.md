# 「Computer Security Fundamentals, 4th Edition」の5章
2021/04/04(Sun) 09:00am-10:30am

## 読書会当日に話したいこと

### Chapter 5. Malware
- 話したいことというより、勉強になったこと
- Diffs between `a virus`, `a worm` and `a Trojan horse`
- a Trojan horseは情報収集活動、バックドアの設置などが目的のため、収集先のデバイスに長期間の潜伏が臨まれる。そのため、a Trojan horse自体は一見怪しい点がないように作られている。

|               | 寄生/感染する? | 自己増殖する？|
|---------------|-------------|-----------|
|a virus        |する          |する        |
|a worm         |しない(単独)    |する       |
|a Trojan horse |しない          |しない      |

- 5章でvirusとwormの違いについて記載されているところ
  - > I would define a virus as any file that can self-replicate and a worm as any program that can propagate without human interference. This is also the most common definition you will find among security experts.

---
## 読書メモ
### Chapter 5. Malware

```
- Understand viruses (worms) and how they propagate, including famous viruses like WannaCry, Rombertik, and Petya
- Have a working knowledge of several specific virus outbreaks
- Understand how virus scanners operate
- Understand what a Trojan horse is and how it operates
- Have a working knowledge of several specific Trojan horse attacks
- Grasp the concept behind the buffer-overflow attack
- Have a better understanding of spyware and how it enters a system
- Defend against each of these attacks through sound practices, antivirus software, and antispyware software
```

- Types of Viruses
  - Macro, Multi-partite, Memory resident, Armored, Sparse infector, Polymorphi, Metamorphic, Boot sector


#### Test Your Skills

- 1. John is a network security administrator for a midsized college. He is trying to explain to a new hire what a virus is. Which of the following is the best definition of virus?
  - D. A program that self-replicates

- 2. Any rapidly spreading virus can reduce the functionality and responsiveness of a network. Isabelle is responsible for cybersecurity at her company. She is concerned that a virus would cause damage to the IT systems. What is the most common damage caused by virus attacks?
  - A. Slowing down networks by the virus traffic
  
- 3. You are trying to form policies for your organization to mitigate the threat of viruses. You want to ensure that you address the most common way for a virus to spread. What is the most common way for a virus to spread?
  - D. By download from a website

- 4. Which of the following is the primary reason that Microsoft Outlook is so often a target for virus attacks?
  - C. It is easy to write programs that access Outlook’s inner mechanisms.
    - > A macro virus is written into a macro in some business application. For example, Microsoft Office allows users to write macros to automate some tasks. Microsoft Outlook is designed so that a programmer can write scripts using a subset of the Visual Basic programming language, called Visual Basic for Applications (VBA).

- 5. Which of the following virus attacks used a multimodal approach?
  - C. Sobig virus

- 6. What factor about the WannaCry virus is especially interesting to security practitioners?
  - A. It could have been prevented with good patch management.
    - > The first reason this virus is noteworthy, is that there was a patch for the vulnerability it exploited, and that patch had been available for weeks. This illustrates why patch management is such an important part of cybersecurity.

- 7. What is the name of the very first virus ever detected?
  - A. Creeper
    - > It is instructive to consider the very first viruses every found. In 1971, Bob Thomas created what is widely believed to be the first computer virus, named Creeper.

- 8. Which of the following reasons most likely enabled the Bagle virus to spread so rapidly?
  - A. The email containing it claimed to be from the system administrator.
    - >  The Bagle virus began to spread rapidly in the fourth quarter of 2003. The email it sent claimed to be from your system administrator. It would tell you that your email account had been infected by a virus and that you should open the attached file to get instructions. 

- 9. What made the Bagle virus so dangerous?
  - B. It disabled antivirus software.
    - > Finally, it would disable processes used by antivirus scanners. In biological terms, this virus took out your computer’s “immune system.” 

- 10. Which of the following is a method that any person can use to protect against virus attacks?
  - D. Never open unknown email attachments.
  - B. Use encrypted transmissions. (My opinion)

- 11. You are trying to develop methods to mitigate the threat of viruses in your company. Which of the following is the safest way to send and receive attachments?
  - A. Use a code word indicating that an attachment is legitimate.
    - > You might even exchange a code word with friends and colleagues. Tell them that if they wish to send you an attachment, they should put the code word in the title of the message. Without seeing the code word, you will not open any attachment

- 12. Shelly is trying to teach new employees how to handle emailed security alerts. Which of the following is true regarding emailed security alerts?
  - B. Most companies do not send alerts via email.
    - > Do not believe “security alerts” that are sent to you. Microsoft does not send out alerts in this manner. Check the Microsoft website regularly, as well as one of the antivirus websites previously mentioned.

- 13. Which of the following is something a Trojan horse might do?
  - A. Open a backdoor for malicious software.

- 14. Jared is explaining various attacks to students in an introduction to cybersecurity class. He wants to make certain they fully understand the different attacks. What does a buffer-overflow attack do?
  - D. It puts more data in a buffer than it can hold.
    - > A buffer-overflow attack happens when someone tries to put more data in a buffer than it was designed to hold.

- 15. What virus exploited buffer overflows?
  - C. Sasser virus
    - > Sasser is an older attack but one that demonstrates the use of a buffer-overflow attack.

- 16. What can you do with a firewall to help protect against virus attacks?
  - B. Shut down all unneeded ports.

- 17. Malek is explaining various malware types to new technical support personnel. He is explaining to them the various types of malware so that they can recognized them. What type of malware is a key logger?
  - D. Spyware
    - > Spyware can be as simple as a cookie used by a website to record a few brief facts about your visit to that website, or it could be of a more insidious type, such as a key logger.

- 18. Which of the following is a step that all computer users should take to protect against virus attacks?
  - D. Install and use antivirus software.

- 19. What is the primary way a virus scanner works?
  - A. By comparing files against a list of known virus profiles
    - > It is therefore important to keep your virus software updated so that you have the most recent list of signatures with which to work.
  

- 20. What other way can a virus scanner work?
  - D. By looking at files for virus-like behavior
    - > The other way in which a virus scanner might check a given PC is to look at the behavior of an executable.

---
- `preventive`
  - adj
  - meaning: designed to keep something undesirable such as illness or harm from occurring.
    - e.g.: "preventive medicine"
    - Syn: inhibitory, preventative, deterrent, pre-emptive, obstructive, precautionary, protective, prophylactic, disease-preventing
- `immune`
  - adj
  - meaning: resistant to a particular infection or toxin owing to the presence of specific antibodies or sensitized white blood cells.
    - e.g.: "they were naturally immune to hepatitis B"
  - meaning: protected or exempt, especially from an obligation or the effects of something.
    - e.g.: "they are immune from legal action"
    - Syn: resistant
- `hoax`
  - > a falsehood deliberately fabricated to masquerade as the truth. It is distinguishable from errors in observation or judgment, rumors, urban legends, pseudosciences, and April Fools' Day events that are passed along in good faith by believers or as jokes.
    - Source: [Hoax - Wikipedia](https://en.wikipedia.org/wiki/Hoax)
- `devastating`
  - adj
  - meaning: highly destructive or damaging.
    - e.g.: "a devastating cyclone"
    - Syn: destructive
- `divluge`
  - verb
  - meaning: make known (private or sensitive information).
    - e.g.: "I do not want to divulge my plans at the moment"
    - Syn: disclose, reveal
- `premise`
  - noun
  - meaning: a previous statement or proposition from which another is inferred or follows as a conclusion.
    - e.g.: "if the premise is true, then the conclusion must be true"
- `propate`
  - verb
  - meaning: breed specimens of (a plant or animal) by natural processes from the parent stock.
    - e.g.: "try propagating your own houseplants from cuttings"
    - Syn: breed, grow
  - meaning: spread and promote (an idea, theory, etc.) widely.
    - e.g.: "the French propagated the idea that the English were drunkards"
    - Syn: spread, disseminate
- `malicious`
  - adj
  - meaning: characterized by malice; intending or intended to do harm.
    - e.g.: "he was found guilty of malicious damage"
- `malice`
  - noun
  - meaning: the desire to harm someone; ill will.
    - e.g.: "I bear no malice towards anybody"
    - Syn: spite, Smalevolence

---
- [マルウェア感染による日経新聞社員らの情報流出についてまとめてみた - piyolog](https://piyolog.hatenadiary.jp/entry/2020/05/13/174643)
  - > 2020年5月8日に流出被害が判明。グループ会社の従業員が使用するPC1台がマルウェアに感染していた。
  - > フリーメールに添付されたファイルを開いたことが原因と報じられている。*1
  - > マルウェア検知システムは導入されていたが、添付ファイルに仕込まれていたマルウェアは検知できなかった。
  - > 発端は感染後の外部への通信などの異常を検知したことによる。 
- [差し込むとマルウェア感染するUSBデバイスが届いた事例についてまとめてみた - piyolog](https://piyolog.hatenadiary.jp/entry/2020/03/30/052613)
# 「Computer Security Fundamentals, 4th Edition」の1章
2021/02/28(Sun) 09:00am-10:30am

## 読書会当日に話したいこと

### Chapter 1. Introduction to Computer Security
- Case Study

---
## 読書メモ
### Chapter 1. Introduction to Computer Security

```
- Identify the top threats to a network: security breaches, denial of service attacks, and malware
- Assess the likelihood of an attack on your network
- Define key terms such as cracker, penetration tester, firewall, and authentication
- Compare and contrast perimeter and layered approaches to network security
- Use online resources to secure your network
```

#### Introduction
```
- How is information safeguarded?
- What are the vulnerabilities to these systems?
- What steps are taken to ensure that these systems and data are safe?
- Who can access my information?
```

####  Concepts and Approaches
- Figure 1.1 The McCumber cube.
  - Source: [Introduction to Computer Security | Introduction | Pearson IT Certification](https://www.pearsonitcertification.com/articles/article.aspx?p=2990398)
<img src="https://i.gyazo.com/c894c34c66e923a61e52d9a1cc968118.jpg" style="max-width:40%;">

- Figure 1.2 The security approach guide.
  -  Source: [Introduction to Computer Security | Introduction | Pearson IT Certification]
   <img src="https://i.gyazo.com/adf854854d9668232a0e9af37aea2b24.jpg" style="max-width:40%;">

#### Test Your Skills  
- Q1. You are trying to explain security to a nontechnical manager. She has taken a rather extreme view of computer security. Which of the following is one of the extreme viewpoints about computer security discussed in this chapter?
  - A. The federal government will handle security.
- Q2. You have just taken over as network security administrator for a small community college. You want to take steps to secure your network. Before you can formulate a defense for a network, what do you need?
  - Author's opinions is "B. A clear picture of the dangers to be defended against", while my opinion is "A. Appropriate security certifications".
- Q3. Mary is teaching an introductory cybersecurity course to freshmen. She is explaining to them the major threats. Which of the following is not one of the three major classes of threats?
  - B. Online auction fraud
- Q4. Being able to define attack terms is an important skill for a cybersecurity professional. What is a computer virus?
  - C. Any program that causes harm to your system
- Q5. Being able to define attack terms is an important skill for a cybersecurity professional. What is spyware?
  - A. Any software that monitors your system
  - C. Any software used to gather intelligence
  - "D. Only software that monitors what websites you visit" is not appropriate, because it contains "only"
    - > Spyware is simply software that literally spies on what you do on your computer. 
    - > your entire Internet browsing history can be tracked. Spyware may also consist of software that takes periodic screenshots of the activity on your computer and sends them to the attacker.
    - cf. [スパイウェアとは？](https://prius.hitachi.co.jp/support/beginner/faq/700043/700043.html)
- Q6. What is a penetration tester?
  - C. A person who hacks a system to test its vulnerabilities
- Q7. Elizabeth is explaining various hacking terms to a class. She is in the process of discussing the history of phone system hacking. What is the term for hacking a phone system?
  - D. Phreaking
    - > One specialty type of hacking involves breaking into telephone systems. This subspecialty of hacking is referred to as phreaking.
- Q8. What is malware?
  - A. Software that has some malicious purpose
    - > Malware is a generic term for software that has a malicious purpose. This section discusses four types of malware: viruses, Trojan horses, spyware, and logic bombs. 
- Q9. What is war-driving?
  - C. Driving looking for wireless networks to hack
    - cf. [ウォードライビング（War Driving） | セコムトラストシステムズのBCP（事業継続計画）用語辞典](https://www.secomtrust.net/secword/wardriving.html)
- Q10. What is the name for the hacking technique that involves using persuasion and deception to get a person to provide information to help compromise security?
  - A. Social engineering
- Q11. There are many threats on the Internet. Which one is currently the most common may change over time, but certain threats have always been more common than others. Which of the following is the most common threat on the Internet?
  - C. Computer viruses
  - D. Illegal software
- Q12. What are the three approaches to security?
  - A. Perimeter, layered, hybrid
    - > Figure 1.2 The security approach guide.
- Q13. Defining your security strategy is an important step in securing a network. You are trying to classify devices based on the approach they take to security. An intrusion detection system is an example of which of the following?
  - B. Perimeter security
- Q14. Which of the following is the most basic security activity?
  - A. Authentication
  - D. Auditing
- Q15. The most desirable approach to security is one that is which of the following?
  - B. Layered and dynamic
- Q16. According to a survey of 223 computer professionals prepared by the Computer Security Institute, which of the following was most often cited as an issue by respondents?
  - D. Internet connection
- Q17. Which of the following types of privacy law affects computer security?
  - C. Any privacy law
- Q18. The first computer incident-response team is affiliated with what university?
  - B. Carnegie-Mellon University
- Q19. Which of the following is the best definition of the term sensitive information?
  - C. Any information that if accessed by unauthorized personnel could damage your organization in any way
- Q20. Which of the following is a major resource for detailed information on a computer virus?
  - C. The F-Secure Virus Library

#### Exercise 1.3: Hacker Terminology
- Alpha geek
  - ギーク界隈のリーダー的存在のギーク
  - cf. [はじめに－－アルファギークとは？［小飼弾のアルファギークに逢ってきた（WEB+DB PRESS plusシリーズ）］｜gihyo.jp … 技術評論社](http://gihyo.jp/magazine/wdpress/plus/978-4-7741-3452-9/0001)
- Grok
  - > [from the novel "Stranger in a Strange Land", by Robert A. Heinlein, where it is a Martian word meaning literally `to drink' and metaphorically `to be one with'] The emphatic form is `grok in fullness'. 1. To understand, usually in a global sense. Connotes intimate and exhaustive knowledge. Contrast zen, which is similar supernal understanding experienced as a single brief flash. See also glark. 2. Used of programs, may connote merely sufficient understanding. "Almost all C compilers grok the void type these days."
    - Source: [The New Hacker's Dictionary - = G =](https://www.outpost9.com/reference/jargon/jargon_22.html#SEC29)
- Red Book
  - > Any of the 1984 standards issued by the CCITT eighth plenary assembly. These include, among other things, the X.400 email spec and the Group 1 through 4 fax standards. 
    - Source: [The New Hacker's Dictionary - = R =](https://www.outpost9.com/reference/jargon/jargon_33.html#SEC40)
  - cf. [Red Bookとは レッドブック： - IT用語辞典バイナリ](https://www.sophia-it.com/content/Red+Book)
- Wank
  - > denoting a clever technique or person or the result of such cleverness
    - Source: [The New Hacker's Dictionary - = W =](https://www.outpost9.com/reference/jargon/jargon_38.html#SEC45)
  - cf. [WANK (computer worm) - Wikipedia](https://en.wikipedia.org/wiki/WANK_(computer_worm))

#### Case Study
- シングルサインオン

----
- `prevalenve`
  - noun  from adjective `prevalent`
  - meaning: widespread, common, or extensive.
- `inextricably`
  -  adv
  - meaning: in a way that is impossible to disentangle or separate.
    - e.g.: "for many top executives, golf and business are inextricably linked" 
- `intertwine`
  - verb
  - meaning: twist or twine together.
    - e.g.: "a net made of cotton intertwined with other natural fibres" 
  - meaning: connect or link (two or more things) closely.
    - e.g.: "as with most traditions, fact and fiction have become inextricably intertwined" 

- Perimeter security
  - > to natural barriers or built fortifications to either keep intruders out or to keep captives contained within the area the boundary surrounds.
    - Source: [Perimeter security - Wikipedia](https://en.wikipedia.org/wiki/Perimeter_security)
  - > ドメインの境界であり、その中でセキュリティ ポリシー、もしくは、セキュリティアーキテクチャが適用される。； すなわち、空間の境界であり、その中で、セキュリティサービスがシステム資源を防護する。
  - Souce: [Internet Security Glossary](https://www.ipa.go.jp/security/rfc/RFC2828-03SJA.html)

---
- [2020年の10大セキュリティ事件、2位に大差をつけた1位は「ドコモ口座」問題 | マイナビニュース](https://news.mynavi.jp/article/20201215-1593933/)
- [ビザスクの情シスが激動の2020年を振り返る | VISASQ TECH BLOG](https://tech.visasq.com/it-team-2020/)

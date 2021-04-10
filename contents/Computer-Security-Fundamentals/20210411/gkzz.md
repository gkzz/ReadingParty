# 「Computer Security Fundamentals, 4th Edition」の6章
2021/04/11(Sun) 09:00am-10:30am

## 読書会当日に話したいこと

### Chapter 6. Techniques Used by Hackers
- ご報告
  - 大変ココロ苦しいのですが、この読書会を次回18日(日)で一旦休会としようと思います。
- 話したいことというより、勉強になったこと
  - 最下部に書いてある「Facebook」での脆弱性の見付け方の記事
  - 学割を使ってpcを20%オフで買った
    - [Dellの学割キャンペーン (小学生から大学生向け） | Dell 日本](https://www.dell.com/ja-jp/shop/student-discount-purchase-program/cp/student-discount-purchase-program)
    - 大学ではofficeを指定
  - Amazonプライムの学生プランの切り替えも
    - https://www.amazon.co.jp/amazonprime?_encoding=UTF8&ms3_c=00319a68e8a36c4b57f03e61ac015551


---
## 読書メモ
### Chapter 6. Techniques Used by Hackers


#### Test Your Skills
- 1. Elizabeth is describing web-based attacks to a group of students in a computer security course. What does an SQL injection attack require?
  - B. Creating an SQL statement that is always true
  - C. Creating an SQL statement that will force access
    - > SQL injection works by putting some SQL into the username and password block that is always true.

- 2. Juan is looking for a vulnerability scanner that is specifically tailored to Windows systems. Which of the following is a vulnerability scanner specifically for Windows systems?
  - A. Nmap, 
    - > A simple Google search for port scanner will reveal a host of well-known, widely used, and often free port scanners. However, the most popular port scanner in the hacking and security community is the free tool Nmap (https://nmap.org). There is a Windows version of it, called Zenmap,

- 3. You are responsible for security on an e-commerce system. You want to mitigate as many attacks as you can. How can you prevent cross-site scripting?
  - A. Filter user input.
    - > Again, such attacks can be prevented by simply filtering all user input. As of this writing, all the major online shopping portals, such as Amazon.com, do filter input and are not susceptible to this attack. However, many smaller sites are still susceptible to cross-site scripting.

- 4. What is an advantage of using Nessus? (Use your favorite search engine to research Nessus to answer this question.)
  - B. It can check for a wide range of vulnerabilities.
    - > Nessus® Professional, the industry’s most widely deployed vulnerability assessment solution helps you reduce your organization’s attack surface and ensure compliance. Nessus features high-speed asset discovery, configuration auditing, target profiling, malware detection, sensitive data discovery and more.
      - Source: [Nessus Vulnerability Scanner - Advantage Industries Can Help](https://www.getadvantage.com/cybersecurity-nessus-vulnerability-scanner/)

5. Perez is exploring different password cracking tools. A friend has told him about ophcrack. ophcrack depends on the attacker doing what?
  - B. Getting domain admin privileges
    - > One must be a domain admin for it to work. So the attacker saves this script to the All Users startup folder. The next time a domain admin logs on to this system, the script will successfully execute. But the attacker may not want to wait until that happens. `In order to speed up the process, the attacker causes some minor problem in the system (changes settings, alters configuration, and so on).` 

6. If you wish to view items that have been removed from a website, what is the best way to do so?
  - D. Use www.archive.org.
    - >  This site, shown in Figure 6.2, archives older versions of websites. The server scours the Web, archiving sites. `The frequency with which a site is archived depends on its popularity.`

7. Malek needs a port scanner so he can scan open ports on his own network. Which of the following is a popular port scanner?
  - D. Nmap
    - > the most popular port scanner in the hacking and security community is the free tool Nmap (https://nmap.org). There is a Windows version of it, called Zenmap,

8. Jane wants to mitigate as many attacks as she can. A colleague suggested that she block ICMP packets. Blocking incoming ICMP packets will prevent what type of scan?
  - B. Ping

9. It is important that you understand cybersecurity terminology, including terms for different actors in cybersecurity. What is the correct term for a person who uses hacking techniques for illegal activities?
  - D. A cracker
    - >  The techniques themselves are not criminal. However, there are people who use hacking techniques to breach systems to steal data, damage systems, or commit other cybercrimes. These people are usually referred to as black hat hackers or crackers.

10. What is the term for a person who hacks into phone systems?
  - C. A phreaker
    - >  These people are termed script kiddies (also sometimes spelled kiddys). Another important term, phreaking, refers to hacking into phone (which predates hacking into computer systems).

- 11. Penelope is teaching an introductory cybersecurity course and is trying to explain the terminology to students. What is the term for a person who uses tools to hack without understanding the underlying technology?
  - A. A script kiddy
    - >  perform some cyber attack without really understanding it. These people are termed script kiddies (also sometimes spelled kiddys). Another important term, phreaking, refers to hacking into phone (which predates hacking into computer systems).

- 12. What is the name for the process of trying to list all the servers on a network?
  - B. Enumeration

- 13. Terrance is trying to enumerate his network resources. Which of the following is a popular enumeration tool?
  - D. Cheops

- 14. Jaron is trying to do a port scan of his own company. He wants to test to see if the company’s security systems will be able to detect his scan. Which of the following is considered the most stealthy port scan?
  - D. Nmap
    - > he most popular port scanner in the hacking and security community is the free tool Nmap (https://nmap.org). There is a Windows version of it, called Zenmap,

- 15. What is the most stealthy way to find out what type of server a website is running?
  - C. Use www.netcraft.com.

---
- `probing`
  - adj
  - meaning: inquiring closely into something; searching.
    - e.g.: "she asks some probing questions"

- `enumerate`
  - verb
  - meaning: mention (a number of things) one by one.
    - e.g.: "there is not space to enumerate all his works"
    - Syn: list, itemize

- `emulate`
  - > In computing, an emulator is hardware or software that enables one computer system (called the host) to behave like another computer system (called the guest). An emulator typically enables the host system to run software or use peripheral devices designed for the guest system. 
    - Source: [Emulator - Wikipedia](https://en.wikipedia.org/wiki/Emulator)
---

- [「バグ報奨金の稼ぎ方」が少しわかりそうな「Facebookに存在するバグ脆弱性レポート」 - GIGAZINE](https://gigazine.net/news/20201215-facebook-subdomain-bug-bounty/)
  - > Abdulridha氏は新型コロナウイルス感染拡大で生まれた時間を利用して、ウェブアプリケーションに侵入して脆弱性を見つけ出すペネトレーションテストの認定試験「OSWE」の資格を取得したとのこと。Facebookのサブドメイン「legal.tapprd.thefacebook.com」内の「HTMLをPDFに変換する機能」の脆弱性を見つけ出し、Facebookから1000ドル(約10万4000円)の報奨金を受け取ったという記事がきっかけとなり、「legal.tapprd.thefacebook.com」へのペネトレーションテストを実行することに決めたそうです。

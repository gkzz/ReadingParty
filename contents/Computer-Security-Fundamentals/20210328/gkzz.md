# 「Computer Security Fundamentals, 4th Edition」の4章
2021/03/28(Sun) 09:00am-10:30am

## 読書会当日に話したいこと

### Chapter 4. Denial of Service Attacks
- tshark(wireshark的なもの)とtcpdumpでパケットキャプチャしてみたｗ
  - 参考：[Wiresharkを使った通信監視（後編）――コマンドラインベースでのパケットキャプチャ | さくらのナレッジ][ref-sakura]

---
## 読書メモ
### Chapter 4. Denial of Service Attacks

```
- Understand how denial of service attacks are accomplished
- Know how certain denial of service attacks work, such as SYN flood, Smurf, and distributed denial of service attacks
- Take specific measures to protect against denial of service attacks
- Know how to defend against specific denial of service attacks
```

#### Test Your Skills  
- 1. When considering the various attacks that can be executed on your system, it is important to understand which attacks are most common. Of the following, which is one of the most common and simplest attacks on a system?
  - A. Denial of service attack
- 2. All DoS attacks are predicated on overwhelming a system’s workload capacity. Therefore, measuring the workload of a system is critical. Which of the following is not a valid way to define a computer’s workload?
  - C. Maximum voltage
    - > . A workload for a computer system may be defined by the number of simultaneous users, the size of files, the speed of data transmission, or the amount of data stored. 

- 3. What do you call a DoS attack launched from several machines simultaneously?
  - D. DDoS attack
    - > A DoS attack that is launched from several different machines is called a distributed denial of service (DDoS) attack.

- 4. It is important to understand the different types of DoS attacks and the symptoms of those attacks. Leaving a connection half open is a symptom of which type of attack?
  - C. SYN flood attack
    - > A SYN flood (half-open attack) is a type of denial-of-service (DDoS) attack which aims to make a server unavailable to legitimate traffic by consuming all available server resources. By repeatedly sending initial connection request (SYN) packets, the attacker is able to overwhelm all available ports on a targeted server machine, causing the targeted device to respond to legitimate traffic sluggishly or not at all.
      - [SYN Flood DDoS Attack | Cloudflare][ref-cloudflare]

- 5. While there are a wide range of different ways to execute a DoS attack, they all are predicated on the same idea. What is the basic concept behind a DoS attack?
  - C. Computers cannot handle large volumes of TCP traffic.
  - D. Computers cannot handle large loads.
    - > Every technology has limits; if you can exceed those limits, then you can take the system offline. This reality underlies the DoS attack. Simply overload the system with requests, and it will no longer be able to respond to legitimate users attempting to access the web server.

- 6. What is the most significant weakness in a DoS attack from the attacker’s viewpoint?
  - D. The attack must be sustained.
    - > The weakness in any DoS attack, from the attacker’s point of view, is that the flood of packets must be sustained. 

- 7. What is the most common class of DoS attacks?
  - A. Distributed denial of service

- 8. A range of countermeasures can help defend against DoS attacks. What are three methods for protecting against SYN flood attacks?
  - A. SYN cookies, RST cookies, and stack tweaking

- 9. Juan is explaining various DoS attacks to security operators at his company. Which attack mentioned in this chapter causes a network to perform a DoS attack on one of its own servers?
  - A. SYN flood

- 10. What is the name for a defense that depends on a hash being sent back to the requesting client?
  - A. Stack tweakingB. RST cookiesC. SYN cookiesD. Hash tweaking

- 11. What type of defense depends on sending the client an incorrect SYN/ACK?
  - B. RST cookies
    - > In this method, the server sends an incorrect SYN+ACK back to the client. The client then generates an RST packet, telling the server that something is wrong. Because the client sends back a packet notifying the server of the error, the server now knows the client request is legitimate and can now accept incoming connections from that client in the normal fashion.

- 12. You are attempting to explain various DoS attacks to a new security technician. You want to make sure she can differentiate between these different attacks and notice the signs of a specific attack. What type of defense depends on changing the server so that unfinished handshaking times out sooner?
  - A. Stack tweaking
    - > Stack tweaking involves altering the TCP stack on the server so that it will take less time to time out when a SYN connection is left incomplete. `Unfortunately, this protective method will just make executing a SYN flood against that target more difficult; to a determined hacker, the attack is still possible.`

- 13. What type of attack is dependent on sending packets that are too large for the server to handle?
  - A. Ping of death
    - > Recall from Chapter 2 that TCP packets are of limited size. In some cases, `simply sending a packet that is too large can shut down a target machine. This action is referred to as the ping of death (PoD).`

- 14. You want to make sure your team can identify the various DoS attack vectors. What type of attack uses the victim’s own network routers to perform a DoS attack on the target?
  - B. Smurf attack

- 15. There have been many different types of attacks over the years. Which of the following is an example of a DDoS attack? 
  - A. MyDoom virus

- 16. How can securing internal routers help protect against DoS attacks?
  - D. It will prevent an attack from propagating across network segments.
    - > If your network is large enough to have internal routers, then you can configure those routers to disallow any traffic that does not originate with your network. 

- 17. What can you do to your internal network routers to help defend against DoS attacks?
  - B. Disallow all traffic that comes from outside the network

- 18. There are classic attacks that, while several years old, are worthy of study due to their significance in the history of cybersecurity. Which of the following was rated by many experts (at the time) to be the fastest growing virus on the Internet?
  - A. MyDoom virus
  - C. Slammer virus

- 19. No attack mitigation strategy is perfect, and you need to allow at least some traffic into and out of your network, or else your network is of no use. What can you do with your firewall to defend against at least some DoS attacks?
  - A. Block all incoming traffic
  - D. Block all incoming ICMP packets
    - > Since DoS/DDoS attacks can be executed via a wide variety of protocols, you can also configure your firewall to disallow any incoming traffic at all, regardless of what protocol or port it occurs on.
    - > There are very few legitimate reasons (...) for an ICMP packet from outside your network to enter your network. 

- 20. You are trying to identify all potential DoS attack vectors. In doing so, you hope to provide mitigation for each of these attack vectors. Why will protecting against Trojan horse attacks reduce DoS attacks?
  - B. If you can stop a Trojan horse attack, you will also stop DoS attacks

    - > The only problem for the hacker is getting the packets started on the target network. This task can be accomplished via some software, such as a virus or Trojan horse, that will begin sending the packets.
    - > Because many distributed DoS attacks depend on “unwitting” computers being used as launch points, one way to reduce such attacks is to protect your computer against virus attacks and Trojan horses. S
---
- `predicate`
  - verb
  - meaning: state, affirm, or assert (something) about the subject of a sentence or an argument of a proposition.
    - e.g.: "a word which predicates something about its subject"
  - meaning: found or base something on.
    - e.g.: "the theory of structure on which later chemistry was predicated"
    - Syn: base, be dependent, found, establish, rest, build, ground
- `legitimate`
  - [../20210321/gkzz.md](../20210321/gkzz.md)
- `symptom`
  - noun
  - meaning: a physical or mental feature which is regarded as indicating a condition of disease, particularly such a feature that is apparent to the patient.
    - e.g.: "dental problems may be a symptom of other illness"
    - Syn: manifestation, indication, indicator, sign, mark, feature, trait
- `sustained`
  - adj
  - meaning: continuing for an extended period or without interruption.
    - e.g.: "several years of sustained economic growth"
- `differentiate`
  - verb
  - meaning: make or become different in the process of growth or development.
    - e.g.: "the receptors are developed and differentiated into sense organs"
    - Syn: transform, metamorphose, evolve, convert, change
- `mitigation`
  - noun
  - meaning: the action of reducing the severity, seriousness, or painfulness of something.
     - e.g.: "the identification and mitigation of pollution"
     - Syn: alleviation, reduction, diminution, lessening, leasing, weakening
---

- [DDoS攻撃について教えてください。 | Questionbox][ref-peing]
- [ASCII.jp：最近は目立ちにくいDDoS攻撃が増加している][ref-ascii]
- [日産自動車のWebサイト閲覧障害についてまとめてみた - piyolog][ref-piyolog]
- [Wiresharkを使った通信監視（後編）――コマンドラインベースでのパケットキャプチャ | さくらのナレッジ][ref-sakura]
- [TCP/IP - TCP 3ウェイハンドシェイク][ref-infraexpart]
- [SYN cookies - Wikipedia][ref-wiki-syn]

[ref-cloudflare]:https://www.cloudflare.com/learning/ddos/syn-flood-ddos-attack/
[ref-peing]:https://peing.net/en/q/8d995b56-837d-41ab-9c65-bd8dd0e11c4f
[ref-ascii]:https://ascii.jp/elem/000/004/016/4016335/
[ref-piyolog]:https://piyolog.hatenadiary.jp/entry/20160116/1452985392

[ref-infraexpart]:https://www.infraexpert.com/study/tcpip9.html
[ref-wiki-syn]:https://ja.wikipedia.org/wiki/SYN_cookies
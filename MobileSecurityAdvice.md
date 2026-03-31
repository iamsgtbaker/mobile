# 8 Steps to Secure Your Mobile Device

Think about the last time you went a full hour without reaching for your phone. Most of us can't. Our mobile devices are how we check email, join meetings, authenticate into work systems, message our families, manage our finances, and navigate our daily lives. They've become the single device we depend on most at home and at work. That makes taking mobile security seriously more important than ever.

The good news is that both Apple and Google have built genuinely strong security and privacy foundations into the iOS and Android platforms. Hardware encryption, biometric authentication, app sandboxing, and real-time threat detection all work to protect you out of the box.

But platform security only goes so far. Outdated software, a click on a dodgy link, or a misconfigured app permission can undo these measures in seconds.

In this post, the Mobile Threat Centre (MTC) outlines 8 practical steps for protecting your personal and work devices today, backed by the threat intelligence that shows why each one matters. None of them require deep technical expertise. Most take a few minutes. Together, they close the gaps that attackers are actively exploiting.

---

## 1. Keep Your OS and Apps Up to Date

This is the single most impactful thing you can do. Software updates patch the exact vulnerabilities that attackers exploit, and right now the threat is not theoretical. Google TAG and Mandiant have documented that commercial spyware vendors routinely exploit n-day vulnerabilities (those already patched) precisely because they know many users delay updates. Every day you defer an update is a day you remain exposed to a known, fixable weakness.

**Threat Intel:**
In March 2026, Google's Threat Intelligence Group and iVerify independently disclosed two spy-grade iOS exploit kits. Coruna, containing 23 exploits across five full attack chains, was originally built for a commercial surveillance vendor before proliferating to state-sponsored and criminal groups, making it the first observed mass exploitation against iOS devices. DarkSword, uncovered weeks later, targets more recent iOS versions (18.4 through 18.7) and has been used by multiple threat actors globally.

On 23 March, DarkSword's source code was leaked on GitHub. Within days, Proofpoint observed a state-sponsored group deploying it in spear-phishing campaigns.

Critically, every vulnerability in both kits had already been patched. Devices running current software were protected. But the scale of exposure is enormous: as of February 2026, 34% of all active iPhones are not running the latest software. That is over 500 million devices potentially running vulnerable versions. In response, Apple has taken the unprecedented step of sending Lock Screen notifications urging immediate updates.

**Take action:** 
Enable automatic updates and install them the day they arrive. This applies to both your operating system and your apps.

- **iOS:** Settings → General → Software Update → [Automatic Updates](https://support.apple.com/en-gb/guide/iphone/iph3e504502/ios)
- **Android:** Settings → System → Software Update → [enable auto-download and install](https://support.google.com/android/answer/7680439)

---

## 2. Restart Your Phone Regularly

A key difference between traditional malware and the advanced mobile exploits we see today is that they typically lack persistence. Rather than embedding themselves permanently on the device, they run entirely in memory. This makes them stealthier, but it also creates a weakness: a reboot clears them.

**Threat Intel:** 
Amnesty International's forensic analysis of Pegasus — the NSO Group's flagship spyware, found operating in 45 countries — has confirmed that recent implants operate without persistence. A reboot removes the active infection and forces the attacker to re-exploit the device from scratch. The same is true of the Coruna and DarkSword exploit kits discussed above.

**Take action:** 
Make a daily reboot part of your routine. It takes 30 seconds and clears any non-persistent threat running in memory.

---

## 3. Be Skeptical of Links, Calls, and Messages

Most people know what phishing is — a fraudulent email designed to trick you into clicking a link or handing over credentials. But on mobile devices, the same attacks arrive through different channels, and they are far more effective.

Smishing is phishing delivered via SMS or messaging apps: a text that looks like it comes from your bank, a delivery service, or a government agency, urging you to tap a link. Vishing is the voice equivalent — a phone call from someone impersonating IT support, your bank, or a senior colleague, pressuring you to share a password, an MFA code, or account details. Both exploit the trust and urgency that mobile communication creates. People are far more likely to act on a text or answer a call than they are to click a suspicious email on their laptop, and attackers know it.

**Threat Intel:** 
Zimperium's 2025 Global Threat Report found that 80% of fraud events now occur through online or mobile platforms. The 2025 Consumer Cyber Readiness Report found that 30% of people who encountered a digital scam in the past year said it began with a text or messaging app, a 20% increase from the year before.

What makes the latest wave particularly dangerous is AI. CrowdStrike's 2025 Global Threat Report found that AI-generated phishing messages achieve a 54% click-through rate, compared to just 12% for human-written ones. Voice phishing surged 442% in the second half of 2024, driven by AI-generated voice clones that can convincingly impersonate executives, IT help desks, and bank representatives.

**Take action:** 
Never tap links in unexpected texts. Never give personal information, passwords, or MFA codes to an unsolicited caller — even if the caller ID looks legitimate. If something feels urgent and unexpected, hang up and contact the organization directly using a number you look up yourself.

- **iOS:** Enable [Filter Unknown Senders](https://support.apple.com/en-gb/guide/iphone/iph203ab0be4/ios) in Messages and [Silence Unknown Callers](https://support.apple.com/en-gb/guide/iphone/iphe4b0f7ba8/ios)
- **Android:** Enable [spam protection in Google Messages](https://support.google.com/messages/answer/9061432) and [Call Screen](https://support.google.com/phoneapp/answer/9118387) on Pixel devices

---

## 4. Guard Your Phone Like You Guard Your Wallet

Phone snatching — the theft of a device from a user's hand while it is unlocked and in use — has evolved from street crime into a sophisticated cyber-physical attack. The phone itself is no longer the prize. What thieves are after is the unlocked access to everything inside it: banking apps, email, authenticator codes, saved passwords, and personal data. Within minutes, a thief with an unlocked phone can drain bank accounts and take over your digital identity.

**Threat Intel:** 
In England and Wales, an estimated 78,000 people had phones snatched on the street in the year ending March 2024 — roughly 200 per day, a 153% increase year-over-year. In London alone, over 70,000 phones were stolen in 2024. In the US, approximately 1.4 million phones were stolen in 2023.

The financial damage goes far beyond the device. A Wall Street Journal investigation documented a systematic theft ring in Minneapolis where criminals observed victims entering their passcode in bars, stole the phone, then changed the Apple ID password, disabled Find My, and drained bank accounts, all within minutes. In London, the method is industrialized: thieves on e-bikes snatch phones from pedestrians, immediately bag them in Faraday pouches to block GPS tracking, and funnel them to middlemen who exploit or resell the devices overseas.

**Take action:**
- **Be aware of your surroundings** — avoid using your phone near busy roads or in crowds; use a phone grip, lanyard, or crossbody case
- **Enable stolen device protection** — limits what a thief can do with an unlocked phone:
  - **iOS:** Settings → Face ID & Passcode → [Stolen Device Protection](https://support.apple.com/en-gb/120340) (set to "Always")
  - **Android:** Settings → Security & Privacy → [Identity Check](https://support.google.com/android/answer/16285498)
- **Enable theft detection** — locks your phone automatically if it is snatched:
  - **Android:** Settings → Security & Privacy → Device Unlock → [Theft Detection Lock](https://support.google.com/android/answer/15604042) (must be manually enabled)
- **Use biometrics in public** — unlock with Face ID or fingerprint, not your passcode, so there is nothing to observe
- **Set separate authentication on banking and sensitive apps** — use Face ID or a distinct PIN within each one
- **If stolen, act immediately** — mark as lost via [iCloud.com](https://www.icloud.com/find) or [android.com/find](https://www.google.com/android/find), change your Apple ID or Google Account password, suspend the SIM, and file a police report with the IMEI

---

## 5. Use Strong Authentication and a Password Manager

Attackers don't need to hack your password if they can steal it, guess it, or reuse one you've already leaked. The reality is that most of us have passwords sitting in old data breaches, and if you've reused any of them, a single breach gives attackers access to multiple accounts. Passkeys and multi-factor authentication exist to close that gap. A password manager ensures every account has a unique, complex password you don't need to remember.

**Threat Intel:** 
CrowdStrike's 2025 Global Threat Report found that 79% of initial access attacks were malware-free. Attackers are not breaking through technical defenses, they are walking through doors opened by stolen or reused credentials. Credential stuffing, where attackers take breached username and password pairs and try them across other services, is automated and operates at massive scale.

Even when users do have multi-factor authentication in place, the wrong type can be bypassed. SMS-based verification codes are vulnerable to SIM swapping — where an attacker convinces your carrier to transfer your number to their device, intercepting every code sent to it. The FBI tracked $26 million in SIM-swap losses in 2024, and the UK's Cifas reported a 1,055% increase in unauthorized SIM swaps in the same year. Passkeys, authenticator apps, and hardware keys are not vulnerable to SIM swapping because they do not rely on your phone number to deliver codes.

**Take action:**
- **Switch to passkeys** for any service that supports them — they are built into both iOS and Android and cannot be phished.
- **Use an authenticator app or hardware key** for everything else; reserve SMS-based codes only for services that offer no alternative.
- **Use a password manager** to generate and store a unique, complex password for every account. Apple Keychain and Google Password Manager are solid built-in options. Third-party managers like 1Password or Bitwarden offer cross-platform flexibility and require their own separate authentication — which matters if your phone is ever stolen.

- **iOS:** Settings → [Your Name] → Sign-In & Security → [Passkeys and Security Keys](https://support.apple.com/en-gb/guide/iphone/iphf538ea8d0/ios)
- **Android:** Google Account → Security → [Passkeys and Security Keys](https://support.google.com/accounts/answer/13548313)

---

## 6. Use Only Official App Stores and Audit Permissions

Sideloaded apps — those installed from outside the official stores — are a major malware vector. But even within official stores, apps routinely request permissions far beyond what they need. A weather app does not need your contacts. A game does not need your microphone. Every unnecessary permission is an additional path for data to leave your device — whether through the app developer, a third-party SDK embedded in the app, or a future compromise.

**Threat Intel:** 
The risk from sideloading is not theoretical. Google's own analysis found that sideloaded apps contain over 50 times more malware than Play Store apps — and in 2025, Play Protect identified 27 million of them, double the previous year.

**Take action:** 
Install apps exclusively from the Apple App Store or Google Play Store. Review permissions regularly and revoke anything that is not essential — particularly location, camera, microphone, contacts, and file access. Both platforms now auto-reset permissions for apps you haven't used recently, but a manual review remains good practice.

- **iOS:** Settings → Privacy & Security → [review permissions by category](https://support.apple.com/en-gb/guide/iphone/iph251e92810/ios)
- **Android:** Settings → Privacy → [Permission Manager](https://support.google.com/android/answer/9431959)

---

## 7. Harden Privacy Settings and Limit Background Data Sharing

Every piece of data your phone exposes is a potential attack surface — whether it is exploited by advertisers, data brokers, or threat actors. Your advertising ID tracks you across apps. Lock screen notifications display MFA codes and messages to anyone nearby. Your phone number anchors your identity across MFA, banking, and account recovery. And your location data flows silently to third parties through apps you use every day. Reducing what your device shares by default limits what an attacker, or an entire industry, can use against you.

**Threat Intel:** 
Most people assume their data stays within the apps they use. NowSecure found that 75% of iOS apps and 70% of Android apps collect sensitive data and share it with third-party tracking domains. That data feeds an industry operating at staggering scale: a 2025 investigation by netzpolitik.org obtained a single day's sample from one US data broker containing 47 million mobile advertising IDs linked to 380 million location data points across 137 countries. A separate investigation found that journalists could track the movements of top EU officials using location data offered as a free sample by a data broker.

**Take action:**
**Delete your advertising ID:**
- **iOS:** Settings → Privacy & Security → Tracking → [disable "Allow Apps to Request to Track"](https://support.apple.com/en-gb/guide/iphone/iph4f4cbd242/ios)
- **Android:** Settings → Security & Privacy → Privacy Controls → Ads → [Delete advertising ID](https://support.google.com/android/answer/3118621)

**Disable lock screen notification previews** — MFA codes, message content, and calendar details visible on a locked screen can be read by anyone nearby.
- **iOS:** Settings → Notifications → Show Previews → [When Unlocked](https://support.apple.com/en-gb/guide/iphone/iph7c3d2150/ios)
- **Android:** Settings → Notifications → [Sensitive Notifications → off](https://support.google.com/android/answer/9079661)

**Protect your phone number** — set a PIN or passcode with your carrier to prevent unauthorized porting, and request a port-freeze or number-lock on your account.

**Restrict location sharing** — set location permissions to "While Using" or "Never" for apps that do not genuinely need continuous access.
- **iOS:** Settings → Privacy & Security → [Location Services](https://support.apple.com/en-gb/guide/iphone/iph3dd5f9be/ios)
- **Android:** Settings → Privacy → Permission Manager → [Location](https://support.google.com/android/answer/6179507)

**Run a quarterly security review** — both platforms offer built-in tools that walk you through connected devices, active sessions, app permissions, and recovery settings.
- **iOS:** Settings → Privacy & Security → [Safety Check](https://support.apple.com/en-gb/guide/iphone/ips2aad835e1/ios)
- **Google:** [Security Checkup](https://myaccount.google.com/security-checkup)

---

## 8. Enable Advanced Protection Programs

Both Apple and Google offer enhanced security modes that go well beyond default settings. These were originally designed for users at elevated risk — journalists, activists, executives — but given the threats outlined in this post, they are worth considering for anyone who wants the strongest available protection on their platform.

These modes involve trade-offs in convenience. Apple Lockdown Mode blocks most message attachments, restricts FaceTime to known contacts, prevents wired connections when locked, and disables complex web technologies — meaning some websites may not render correctly. Google Advanced Protection enforces Play Protect, blocks sideloading, disables 2G connectivity, forces HTTPS in Chrome, and enables automatic inactivity reboot after 72 hours — some third-party apps that rely on accessibility permissions may not function. For most users, these limitations are minor relative to the protection gained.

It is also worth considering a mobile threat detection (MTD) tool to periodically scan your device for indicators of compromise. Protection modes harden your device, but they do not detect threats that may already be present.

**Threat Intel:** 
These modes deliver measurable protection against the most serious threats in the wild today. In January 2026, the FBI's forensic team confirmed in court documents that it could not extract data from a journalist's iPhone that had Lockdown Mode enabled. Both the Coruna and DarkSword exploit kits — the most significant iOS threats discovered in 2025–2026 — skip execution entirely on devices with Lockdown Mode active. On Android, the EFF recommends Advanced Protection for anyone at elevated risk, and Google Play Protect — which is enforced under Advanced Protection — scans over 350 billion apps daily.

**Take action:**
- **Enable Lockdown Mode (iOS):** Settings → Privacy & Security → [Lockdown Mode](https://support.apple.com/en-gb/105120)
- **Enable Advanced Protection (Android):** Settings → Security & Privacy → [Advanced Protection](https://support.google.com/android/answer/16339980)
- **Scan your device periodically** with a mobile threat detection tool such as [iVerify Basic](https://iverify.io) (free, iOS and Android)

---

## The Bottom Line

The threats are real, but so are the defenses. Start with three steps today: update your OS, enable Stolen Device Protection or Identity Check, and restart your phone. Each one closes a door that an attacker would otherwise walk through.

For more information or guidance on any of the advice in this post, reach out to the Mobile Threat Centre team. We're happy to discuss and guide you through this.

---

*THCD Cyber Threat Operations — Mobile Threat Center, March 2026*

**Sources:**

- [Google Threat Intelligence Group (GTIG), "The Proliferation of DarkSword," March 2026](https://cloud.google.com/blog/topics/threat-intelligence/darksword-ios-exploit-chain)
- [iVerify, "Inside DarkSword: A New iOS Exploit Kit," March 2026](https://iverify.io/blog/darksword-ios-exploit-kit-explained)
- [iVerify, "Coruna: Inside the Nation-State-Grade iOS Exploit Kit," March 2026](https://iverify.io/press-releases/first-known-mass-ios-attack)
- [Proofpoint / The Hacker News, "TA446 Deploys DarkSword iOS Exploit Kit," March 2026](https://thehackernews.com/2026/03/ta446-deploys-leaked-darksword-ios.html)
- [TechCrunch, "Someone has publicly leaked an exploit kit that can hack millions of iPhones," March 2026](https://techcrunch.com/2026/03/23/someone-has-publicly-leaked-an-exploit-kit-that-can-hack-millions-of-iphones/)
- [Apple, iOS adoption data, February 2026](https://developer.apple.com/support/app-store/)
- [Google TAG & Mandiant, "Buying Spying: Commercial Surveillance Vendors," 2024](https://blog.google/threat-analysis-group/commercial-surveillance-vendors-google-tag-report/)
- [Amnesty International, forensic methodology for Pegasus detection](https://www.amnesty.org/en/latest/research/2021/07/forensic-methodology-report-how-to-catch-nso-groups-pegasus/)
- [Citizen Lab, "Hide and Seek: Tracking NSO Group's Pegasus Spyware to Operations in 45 Countries"](https://citizenlab.ca/research/hide-and-seek-tracking-nso-groups-pegasus-spyware-to-operations-in-45-countries/)
- [CrowdStrike, 2025 Global Threat Report](https://www.crowdstrike.com/en-us/resources/reports/)
- [FBI Internet Crime Complaint Center (IC3), Annual Report 2024](https://www.ic3.gov/AnnualReport/Reports/2024_IC3Report.pdf)
- [Zimperium, 2025 Global Mobile Threat Report](https://zimperium.com/resources/mobile-becomes-the-chosen-attack-vector-for-enterprises-zimperium-researchers-find)
- [2025 Consumer Cyber Readiness Report](https://www.consumerreports.org/electronics/digital-security/)
- [Wall Street Journal (Stern & Nguyen), iPhone theft investigations, 2023](https://www.wsj.com/tech/personal-tech/)
- [UK House of Commons Library, Phone Theft (CDP-2025-0150)](https://commonslibrary.parliament.uk/)
- [Metropolitan Police, operational data on phone theft in London](https://www.met.police.uk/)
- [Cifas, Fraudscape 2025](https://www.cifas.org.uk/research/)
- [Google, Play Protect documentation](https://developers.google.com/android/play-protect)
- [Google Security Blog, "Keeping Google Play & Android App Ecosystems Safe in 2025," February 2026](https://security.googleblog.com/2026/02/keeping-google-play-android-app-ecosystem-safe-2025.html)
- [EFF, "Google's Advanced Protection Arrives on Android: Should You Use It?" June 2025](https://www.eff.org/deeplinks/2025/06/googles-advanced-protection-arrives-android-should-you-use-it)
- [NowSecure, mobile app privacy research 2025](https://www.nowsecure.com/)
- [netzpolitik.org, "Databroker Files: New data set reveals 40,000 apps behind location tracking," January 2025](https://netzpolitik.org/2025/databroker-files-new-data-set-reveals-40000-apps-behind-location-tracking/)
- [netzpolitik.org / TechCrunch, "Phone location data of top EU officials for sale," November 2025](https://techcrunch.com/2025/11/04/phone-location-data-of-top-eu-officials-for-sale-report-finds/)
- [iVerify, "Mobile Threat Investigation Uncovers New Pegasus Samples," 2024](https://iverify.io/blog/iverify-mobile-threat-investigation-uncovers-new-pegasus-samples)

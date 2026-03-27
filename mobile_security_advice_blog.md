# 15 Ways to Protect Your Phone From Cyber Threats

**Your phone is your most personal device — and your most exposed one.**

---

You probably don't think of your phone as a high-value target. But consider what's on it right now: your email, your bank accounts, your authenticator apps, your photos, your passwords, your work Slack, maybe even your VPN. If someone gained access to all of that in the next five minutes, how much damage could they do?

The answer, based on documented cases, is a lot. And the threats are growing fast.

In 2024, Kaspersky detected 33.3 million mobile malware attacks globally. The FBI received over 193,000 phishing complaints — the most reported cybercrime category — with $70 million in losses. CrowdStrike's 2025 Global Threat Report found that voice phishing (vishing) attacks exploded by 442% in the second half of 2024, and that AI-generated phishing messages now achieve a 54% click-through rate compared to just 12% for human-written ones.

Mobile devices are now the primary way most of us access sensitive information, but they remain among the least protected endpoints we use. The good news: the most effective defences are straightforward and take minutes to set up.

Here are 15 practical steps to secure your personal phone.

## 1. Update Your Phone and Apps Immediately

This is the single most impactful thing you can do. Software updates patch the exact vulnerabilities that attackers exploit — and right now, the threat is not theoretical.

In March 2026, Google's Threat Intelligence Group and iVerify independently disclosed Coruna, a spy-grade iOS exploit kit containing 23 exploits across five full attack chains, targeting iPhones running iOS 13 through 17.2.1. Originally developed for a commercial surveillance vendor, the kit proliferated to Russian state-sponsored attackers targeting Ukrainian websites and then to Chinese cybercriminals running fake finance websites. iVerify called it the first observed mass exploitation against iOS devices — meaning anyone visiting a compromised website with a vulnerable iPhone could be infected. Critically, every vulnerability in Coruna had already been patched in current iOS versions. Devices that were up to date were protected.

Weeks later, a second exploit kit called DarkSword was uncovered, targeting more recent iOS versions (18.4 through 18.7) and used by multiple threat actors in Ukraine, Saudi Arabia, Turkey, and Malaysia. Then, on March 23, someone leaked DarkSword's code on GitHub, making it freely available to anyone. iVerify's co-founder Matthias Frielingsdorf warned: "This is bad. The exploits will work out of the box. There is no iOS expertise required." Apple confirmed the exploits target devices running older, out-of-date operating systems and urged users to update immediately. Apple also confirmed that Lockdown Mode blocks these specific attacks.

The combined impact of Coruna and DarkSword likely affects hundreds of millions of unpatched devices. The single most important thing you can do: update now, and enable automatic updates so you never fall behind again.

## 2. Use Passkeys or Strong Multi-Factor Authentication

Passwords alone aren't enough anymore. Where available, switch to passkeys — they're built into both iOS and Android and can't be phished. For accounts that don't support passkeys, enable multi-factor authentication using an authenticator app (like Microsoft Authenticator or Authy) or a hardware security key.

Avoid SMS-based verification codes where you can. The FBI tracked $26 million in SIM-swap losses in 2024 — attacks where criminals take over your phone number and intercept your text-based codes. An authenticator app or passkey eliminates that risk entirely.

## 3. Lock Down Your Lock Screen

Your device passcode is the cryptographic key that protects everything on your phone. Use at least a 6-digit PIN, or better yet, an alphanumeric password. Enable Face ID or fingerprint unlock for daily convenience, but understand that the passcode is the master key — never share it, and be careful about entering it where someone could watch.

Apple's Stolen Device Protection feature exists because of a documented wave of thefts where criminals observed victims entering their passcode in bars, then stole the phone and drained their bank accounts within minutes. Enable it (Settings → Face ID & Passcode → Stolen Device Protection → "Always"). On Android, enable Identity Check (Settings → Security & Privacy → Identity Check).

## 4. Only Install Apps From Official Stores

Google's own analysis found that sideloaded apps — those installed from outside the Play Store — contain over 50 times more malware than Play Store apps. In 2025, Google Play Protect identified 27 million malicious sideloaded apps, up from 13 million in 2024. Stick to the Apple App Store or Google Play Store, and be sceptical even there — scrutinise permissions before installing anything.

## 5. Audit Your App Permissions

Many apps request access to your camera, microphone, location, contacts, and files that they don't actually need. A weather app doesn't need your contacts. A game doesn't need your microphone.

Review permissions regularly. On iOS, go to Settings → Privacy & Security. On Android, go to Settings → Privacy → Permission Manager. Revoke anything that isn't essential. Both platforms now auto-reset permissions for apps you haven't used in a while.

## 6. Turn On Advanced Protection Features

Both Apple and Google offer enhanced security modes that go well beyond default settings.

**Apple Lockdown Mode** dramatically reduces your phone's attack surface by disabling complex web technologies, blocking most message attachments, and restricting connections. In January 2026, the FBI's forensic team confirmed in court documents that it could not extract data from a journalist's iPhone that had Lockdown Mode enabled. Notably, both the Coruna and DarkSword exploit kits — the most significant iOS threats discovered in 2025–2026 — skip execution on devices with Lockdown Mode active. Apple confirmed that Lockdown Mode blocks these specific attacks.

**Google Advanced Protection** enforces Play Protect, blocks sideloading, disables 2G connectivity (which is vulnerable to interception), and forces HTTPS in Chrome. The EFF recommends it for anyone facing elevated risk.

These modes involve trade-offs in convenience. But if you handle sensitive information — and most of us do — they're worth considering.

## 7. Enable Encrypted Backups

If your phone is lost, stolen, or wiped, a current backup means you can recover your data. On iOS, enable Advanced Data Protection for iCloud — this provides end-to-end encryption for your backups, photos, notes, and most iCloud data. On Android, enable Google backup in Settings → System → Backup.

Make sure Find My iPhone or Find My Device is turned on so you can remotely locate, lock, or erase a stolen device.

## 8. Be Ruthlessly Sceptical of Links, Calls, and Messages

Smishing (SMS phishing) click-through rates range from 19–36%, far higher than email phishing at 2–4%. People are dramatically more likely to tap a link on their phone than click one on their laptop. Attackers know this.

Never tap links in unexpected texts. Never give personal information, passwords, or MFA codes to someone who calls you — even if the caller ID looks legitimate. CrowdStrike found that attackers are now using AI-generated voice clones to impersonate executives and IT help desks. If something feels urgent and unexpected, hang up and call the organisation directly using a number you look up yourself.

## 9. Use a Password Manager

CrowdStrike's 2025 report found that 79% of initial access attacks were malware-free, relying on stolen or reused credentials. If you use the same password across multiple services, a single breach gives attackers the keys to everything.

Use a password manager to generate and store a unique, complex password for every account. Apple Keychain and Google Password Manager are solid built-in options. Third-party managers like 1Password or Bitwarden offer cross-platform flexibility and the advantage of requiring their own separate authentication — which matters if your phone is ever stolen.

## 10. Protect Your Phone Number

Your phone number is tied to MFA, banking, and account recovery. If someone takes it over, they can intercept your verification codes and reset your passwords.

Set a PIN or passcode with your carrier to prevent unauthorised porting. If your phone supports eSIM, prefer it over a physical SIM — eSIMs have additional transfer protections. Contact your carrier to ask about a port-freeze or number-lock on your account. The UK saw a 1,055% increase in unauthorised SIM swaps in 2024.

## 11. Use Encrypted Messaging for Sensitive Conversations

Standard SMS is transmitted in plaintext and can be intercepted. For sensitive personal or professional communications, use an end-to-end encrypted messenger. Signal is widely regarded as the most secure option. iMessage provides strong encryption between Apple devices. WhatsApp uses Signal's protocol but collects more metadata.

## 12. Minimise Your Data Footprint

Your phone's advertising ID is the mechanism that lets advertisers and data brokers track you across apps. NowSecure found that 75% of iOS apps and 70% of Android apps both collect sensitive data and share it with tracking domains.

Delete your advertising ID. On iOS: Settings → Privacy & Security → Tracking → disable "Allow Apps to Request to Track." On Android: Settings → Privacy → Ads → "Delete advertising ID." Set location permissions to "While Using" or "Never" for apps that don't genuinely need it.

## 13. Use a Privacy-Respecting Browser and Encrypted DNS

Your mobile browser is both an attack surface and a tracking vector. Use one with strong privacy defaults — Safari with tracking protections enabled on iOS, or Brave on either platform. Enable encrypted DNS to prevent your network operator from seeing your browsing queries. On Android: Settings → Network & Internet → Private DNS → set to a trusted provider like dns.quad9.net.

## 14. Restart Your Phone Daily

This one sounds almost too simple, but it has real security value. Many advanced mobile exploits — including most commercial spyware implants and the payloads delivered by exploit kits like Coruna — do not survive a device reboot because they lack persistence on modern iOS and Android. iVerify's March 2026 advisory on the Coruna campaign explicitly recommended daily reboots as the best defence for people without access to mobile security teams. Google's Advanced Protection for Android now includes an automatic reboot if the device has been locked for 72 hours. A daily restart takes 30 seconds and clears non-persistent threats.

## 15. Consider a Mobile Threat Detection Tool

iVerify Basic is a free app for iOS and Android that lets you scan your device for indicators of compromise, including commercial spyware like Pegasus. Their investigations found that approximately half of the Pegasus-infected devices they identified had not received Apple's Threat Notifications — those users would never have known they were compromised without proactive scanning. The infected users included professionals in finance, government, logistics, and real estate, not just the traditional civil society targets.

## Guard Your Phone Like You Guard Your Wallet

There's one threat that no software update can fully prevent: someone physically taking your phone out of your hand while you're using it.

Phone snatching — the theft of an unlocked device from a user's hand — has exploded globally. In England and Wales, an estimated 78,000 people had phones snatched on the street in the year ending March 2024, roughly 200 per day, a 153% increase year-over-year. In London alone, over 70,000 phones were stolen in 2024. In the US, approximately 1.4 million phones were stolen in 2023. Only 12% of stolen phones are ever recovered.

The financial damage goes far beyond the device. A Wall Street Journal investigation documented a systematic theft ring in Minneapolis where criminals observed victims entering their passcode at bars, stole the phone, then changed the Apple ID password, disabled Find My, and drained bank accounts — all within minutes. One victim lost $10,000. The thief, Aaron Johnson, stole hundreds of phones in about a year and described his methods on camera. Dozens of additional victims across multiple US cities contacted the WSJ to confirm identical experiences.

In London, the method is industrialised: thieves on e-bikes snatch phones from pedestrians' hands, immediately bag them in Faraday pouches to block GPS, and funnel them to middlemen. One victim's phone appeared in Dubai five days later. The scale prompted the UK Home Secretary to host a national summit, the Metropolitan Police to launch dedicated operations, and new legislation giving police powers to search for GPS-tracked stolen phones.

For the security-conscious, the key mitigations are: use biometrics (not your passcode) to unlock in public so there's nothing to observe; enable Stolen Device Protection on iOS (set to "Always") or Identity Check on Android so that even with an unlocked phone, a thief can't change your account passwords without your face or fingerprint; set separate authentication on banking apps; and use a third-party password manager rather than relying solely on iCloud Keychain. A phone grip, lanyard, or crossbody case makes the grab-and-ride-away dramatically harder. And Android's Theft Detection Lock uses on-device AI to detect the motion of a snatch-and-run and automatically lock the screen.

The takeaway: your phone is now worth more than your wallet to a thief — not for the hardware, but for the digital life inside it. Be conscious of how and where you use it.

## A Note on Device Choice

The hardware matters too. Never use a device that has passed its security update end-of-life — it can no longer receive patches for known vulnerabilities. Google Pixel phones (8 and later) offer a 7-year update guarantee, a dedicated Titan security chip, and the strongest Android hardware security. iPhones with Face ID running the latest iOS provide excellent baseline protection. As Privacy Guides puts it: a smartphone with the latest operating system will always be more secure than an old phone with an antivirus app.

## The Bottom Line

None of these steps require deep technical knowledge. Most take a few minutes. Together, they dramatically reduce your exposure to the threats that are actually hitting people right now — phishing, credential theft, SIM swapping, device theft, and background data harvesting.

Your phone carries more access than your laptop, holds more personal information than your wallet, and goes everywhere you do. It deserves the same level of protection.

Start with three things today: enable Stolen Device Protection or Identity Check, check your app permissions, and turn on automatic updates. Then work through the rest of this list when you have time. Each step closes a door that an attacker would otherwise walk through.

---

*Cyber Threat Operations — Mobile Threat Centre, March 2026*

*Sources: CrowdStrike Global Threat Report 2025; CrowdStrike 2026 Global Threat Report; FBI IC3 Annual Report 2024; Kaspersky Mobile Threat Landscape 2025; iVerify threat investigations 2024–2026; Google Threat Intelligence Group (GTIG), Coruna and DarkSword analyses, March 2026; Lookout, DarkSword threat intelligence, March 2026; Google TAG & Mandiant zero-day reports; Apple Platform Security Guide; Google Security Blog; Wall Street Journal (Stern & Nguyen), iPhone theft investigations, 2023; UK House of Commons Library (CDP-2025-0150); UK Parliament Hansard, July 2025; Metropolitan Police operational data; NowSecure mobile app privacy research 2025; Privacy Guides (privacyguides.org); EFF Surveillance Self-Defense guides; Cifas Fraudscape 2025; TechCrunch, DarkSword leak reporting, March 2026.*

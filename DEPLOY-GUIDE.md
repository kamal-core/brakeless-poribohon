# GitHub → Vercel Deploy Guide — ব্রেক লেস পরিবহন
### মোবাইল/কম্পিউটার যেকোনো একটা দিয়েই করা যাবে। মোট সময় আনুমানিক ১০–১৫ মিনিট।

এই গেমটা একটাই `index.html` ফাইল — কোনো build/install লাগে না। তাই পদ্ধতিটা সহজ:
**আগে GitHub-এ ফাইল রাখা → তারপর Vercel GitHub থেকে টেনে লাইভ লিংক বানিয়ে দেবে।**
একবার সেটআপ হলে পরে গেম আপডেট করলে GitHub-এ নতুন ফাইল দিলেই Vercel নিজে নিজে আবার লাইভ করে দেবে (auto-deploy)।

---

## ধাপ ১ — GitHub অ্যাকাউন্ট (না থাকলে)
1. মোবাইল/PC ব্রাউজারে যান: **github.com**
2. Sign up → ইমেইল, পাসওয়ার্ড, username দিন (username-টা মনে রাখবেন, লিংকে থাকবে)
3. ইমেইলে আসা কোড দিয়ে verify করুন

## ধাপ ২ — নতুন Repository তৈরি
1. GitHub-এ লগইন করে ডানদিকের **+** → **New repository**
2. Repository name: `brakeless-poribohon`
3. **Public** সিলেক্ট করুন (Public না হলে ফ্রি Vercel-এ সমস্যা হতে পারে)
4. "Add a README file" — চাইলে টিক দিন, না দিলেও চলবে
5. **Create repository** চাপুন

## ধাপ ৩ — গেমের ফাইল আপলোড
1. নতুন repo-র পেজে **Add file → Upload files**
2. Muse-এর দেওয়া ফোল্ডার থেকে এই ফাইলগুলো টেনে দিন / Choose files দিয়ে সিলেক্ট করুন:
   - `index.html` ← **এটাই আসল গেম, এটা বাদ দেওয়া যাবে না**
   - `lib` ফোল্ডারটা পুরোটা ← এর ভিতরে গেমের 3D ইঞ্জিন (`lib/three.module.js`), **এটা বাদ দিলে গেম চলবেই না**
   - `images` ফোল্ডারটা পুরোটা ← About-এর ছবি এর ভিতরে (`images/kamal_photo.png`), **এটা বাদ দিলে About-এ ছবি আসবে না**
   - `README.md`, `DEPLOY-GUIDE.md`, `FEATURE-CATALOGUE.md`
3. নিচে **Commit changes** চাপুন — ব্যাস, GitHub-এ গেম উঠে গেল
4. যাচাই: repo-তে `index.html` দেখা যাচ্ছে কিনা দেখুন

> টিপ: একটা ফাইল বাদ পড়লে আবার Add file → Upload files দিয়ে একইভাবে দিলেই হবে, পুরনো ফাইল replace হয়ে যাবে।

## ধাপ ৪ — Vercel অ্যাকাউন্ট + Deploy
1. ব্রাউজারে যান: **vercel.com**
2. **Sign Up / Log In → Continue with GitHub** (আলাদা পাসওয়ার্ড লাগবে না, GitHub দিয়েই লগইন)
3. Dashboard-এ **Add New → Project**
4. আপনার `brakeless-poribohon` repo-র পাশে **Import** চাপুন
5. সেটিংস — **কিছু বদলানোর দরকার নেই**, কারণ build step নেই:
   - Framework Preset: **Other**
   - Build Command: **খালি** রাখুন
   - Output Directory: **খালি** রাখুন
6. **Deploy** চাপুন → ১ মিনিটের মতো অপেক্ষা → 🎉 "Congratulations!" পেজ আসবে

## ধাপ ৫ — লিংক শেয়ার করে মানুষকে খেলতে দিন
- Deploy শেষে Vercel একটা লিংক দেবে, যেমন: `https://brakeless-poribohon.vercel.app`
- **এই লিংকটাই শেয়ার করবেন** — Facebook পোস্ট, YouTube description, WhatsApp — যেখানে খুশি
- লিংক খুললেই সরাসরি গেম চলবে, কারো কিছু install করা লাগবে না

## পরে আপডেট করবেন যেভাবে (v2 এলে)
1. Muse নতুন `index.html` দেবে
2. GitHub repo → `index.html` ফাইলে ক্লিক → **⋯ / Edit (পেন্সিল) নয়**, সবচেয়ে সহজ: **Add file → Upload files** দিয়ে নতুন ফাইলটা আবার দিন (same name = replace) → Commit
3. Vercel ১ মিনিটের মধ্যে নিজে নিজে নতুন version লাইভ করে দেবে — Vercel-এ আর কিছু করা লাগবে না

## সমস্যা হলে
| সমস্যা | সমাধান |
|---|---|
| Vercel-এ repo দেখা যাচ্ছে না | Vercel Import পেজে "Adjust GitHub App Permissions" দিয়ে repo-টার access দিন |
| লিংক খুললে 404 | GitHub repo-তে `index.html` ঠিক নামে আছে কিনা দেখুন (index.html — বানান/ছোট হাতের অক্ষর হুবহু) |
| গেম সাদা/কালো স্ক্রিন | GitHub-এ `lib` ফোল্ডারসহ সব ফাইল উঠেছে কিনা দেখুন — গেমের সবকিছু লোকাল ফাইলে, CDN লাগে না |
| পুরনো version দেখাচ্ছে | ব্রাউজারে hard refresh: PC-তে Ctrl+Shift+R, মোবাইলে cache clear |

## নিজের ডোমেইন (চাইলে, পরে)
Vercel Project → Settings → Domains → নিজের কেনা ডোমেইন যোগ করা যাবে (যেমন brakelessporibohon.com)। ফ্রি `*.vercel.app` লিংক দিয়েই শুরু করা যথেষ্ট।

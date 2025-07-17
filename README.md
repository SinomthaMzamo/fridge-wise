
# README #
# 🧊 FridgeWise

**Smart shared fridge tracker** for small offices. Use image recognition and simple inputs to track ownership, expiry, and availability of fridge items — no more unlabeled leftovers or fridge wars.

### What is this repository for? ###
> Like Checkers Sixty60, but for your communal fridge. 📦🥪
---

## 🚀 Features
- 📸 **Scan item photos** using AWS Rekognition
- ✍️ Add fridge items with owner, expiry, and communal/private flag
- 📦 View all items with filters (communal, mine, expired, etc.)
- 🧹 Remove or mark items as taken/expired
- 🧠 Image label matching with Rekognition (detect text + object)
- 💾 Optional image storage on AWS S3
- 📅 Optional expiry notifications (via email or Slack)

### Contribution guidelines ###
---

* Writing tests
* Code review
* Other guidelines
## 🧱 Tech Stack

### Frontend
- [Angular](https://angular.io/)
- TailwindCSS or Bootstrap (optional)
- Hosted on AWS S3 + CloudFront

### Backend
- Node.js + Express + TypeScript
- AWS SDK (S3, Rekognition)
- PostgreSQL (via RDS or Supabase)
- Hosted on Elastic Beanstalk or EC2

---

## 🌩 AWS Services Used

| Service       | Purpose                         |
|---------------|----------------------------------|
| S3            | Store uploaded item images       |
| Rekognition   | Detect labels and text in images |
| RDS / Supabase| Store item metadata              |
| IAM           | Secure API and S3 interactions   |
| SES / SNS     | (Optional) Expiry reminders      |
| Lambda        | (Optional) Background cleanup or alerts |

---

## 🗂 Project Structure

```

fridgemate/
├── backend/               # Node.js API
│   ├── controllers/
│   ├── routes/
│   ├── services/
│   └── db/
├── frontend/              # Angular UI
│   ├── src/
│   └── ...
├── infrastructure/        # (Optional) CDK or CloudFormation
└── README.md

````

---

## ⚙️ Setup

### Prerequisites
- Node.js 18+
- Angular CLI
- PostgreSQL or Supabase
- AWS account with S3 + Rekognition enabled
- AWS CLI configured with credentials

### Backend

```bash
cd backend
npm install
cp .env.example .env
# Fill in AWS keys, DB creds, S3 bucket name, etc.
npm run dev
````

### Frontend

```bash
cd frontend
npm install
ng serve
```

---

## 🧪 Key Endpoints

| Method | Route          | Purpose                       |
| ------ | -------------- | ----------------------------- |
| GET    | `/items`       | List all fridge items         |
| POST   | `/items`       | Add new item                  |
| DELETE | `/items/:id`   | Remove item                   |
| POST   | `/scan`        | Analyze image via Rekognition |
| GET    | `/presign-url` | Get S3 signed upload URL      |

---

## 📸 Image Scanning Logic

* Upload image → store in S3
* Send image to Rekognition:

  * `detectLabels` for general objects
  * `detectText` for printed labels (e.g., “Alpro”, “Ceres”)
* Backend matches label/text against items in DB

---

## 📈 Roadmap

* [x] MVP UI with filters
* [x] Image scanning integration
* [ ] User auth (Cognito or name entry)
* [ ] Expiry reminders (SES / Slack)
* [ ] Offline-capable PWA
* [ ] QR code fridge access

---

## 🤝 Contributing

Pull requests are welcome! This started as a weekend project to solve a real office problem, but it could be generalised for any shared environment.

---

## 📜 License

MIT

---

## 🙋‍♀️ Credits

Built by Sinomtha to solve the “**Whose lunch is this?**” problem at the office.
Inspired by Checkers Sixty60 + AWS power 💪

---

## 💡 Tip

> Want to scan barcodes or handwritten notes? See [Limitations](#limitations) in the wiki for Rekognition trade-offs.

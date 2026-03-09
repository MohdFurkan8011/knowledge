## Snowball
Snowball storage on AWS refers to a physical data transport solution called AWS Snowball, part of the AWS Snow Family offered by Amazon Web Services.
It’s designed to move large amounts of data (terabytes to petabytes) into and out of AWS securely and faster than transferring over the internet.

**What It Is**

AWS ships you a rugged physical device. You:
- Connect it to your local network.
- Copy your data onto it.
- Ship it back to AWS.
- AWS uploads the data into your cloud storage (like Amazon S3).

**Why Use Snowball?**

It’s useful when:

- 📦 You have huge data volumes (e.g., 100 TB+)
- 🐢 Internet transfer would take weeks or months
- 🔐 You need secure, encrypted transfer
- 🏢 You’re migrating a data center to AWS
- 🌍 You’re collecting data in remote locations

**Snowball vs Snowmobile**
For extreme scale, AWS offers AWS Snowmobile, which is literally a shipping container pulled by a truck for moving exabytes of data.
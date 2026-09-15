[225.md](https://github.com/user-attachments/files/32227879/225.md)
# Cloud Assignment Answers

## 1. Cloud in your own words
You’re renting computing power and storage from big companies that run massive data centres. You use it over the internet and only pay for what you need. Unlike buying your own computer, you don’t own or maintain any hardware.

## 2. Traditional → Cloud → Containers
Each stage fixed the previous one’s waste and inflexibility. Traditional servers sat mostly idle and were slow to expand. Virtualisation packed more onto one machine. Cloud made capacity available on demand. Containers made apps even lighter and faster to start and move.

## 3. Deployment vs Service models
Deployment models answer *where* the infrastructure lives (on-prem, private, public, hybrid, multi).  
Service models answer *how much* the provider manages for you (IaaS, PaaS, SaaS).  
Example of public cloud + SaaS: Microsoft 365 / Outlook / Teams.

## 4. The Shared Responsibility Model
The cloud provider secures the physical data centres, hardware, and the core platform. You remain responsible for your data, accounts, access rights, and how you configure the services. Moving to the cloud does not hand over your security duties. Even in SaaS you still control who can log in and what data is shared.  

Real example: the 2019 Capital One breach happened because a misconfigured firewall and overly permissive IAM role let an attacker reach private S3 buckets — the customer’s configuration error, not an AWS failure.

## 5. Why organisations still hesitate
- Strict data-residency or regulatory rules (e.g. GDPR) that require data to stay in a specific country or under direct control.
- Desire to avoid lock-in to one vendor or to keep using expensive on-prem hardware they have already paid for.

## 6. Cloud in an entry-level tech role
- A user calls the helpdesk because they can’t sign into Microsoft 365 or Teams — you reset MFA or check Azure AD sign-in logs.
- An alert appears for a suspicious login to a cloud identity, or a customer’s files in an S3/Azure storage account suddenly become inaccessible and you have to investigate permissions.

## 7. Your personal takeaway
I’ll stop treating “the cloud” as something abstract. It’s just someone else’s physical servers, and the security mistakes that matter most are usually the ones we make in configuration and access control.

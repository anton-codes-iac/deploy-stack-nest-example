# NestJS + AWS Fargate & RDS (via deploy-stack) ☁️🚀

> A production-grade example of a modern NestJS application deployed to AWS ECS Fargate with an optional managed PostgreSQL database, generated instantly using the [nest-deploy-stack](https://www.npmjs.com/package/nest-deploy-stack) schematic.

[![NestJS](https://img.shields.io/badge/nestjs-E0234E?style=flat&logo=nestjs&logoColor=white)](https://nestjs.com/)
[![deploy-stack](https://img.shields.io/badge/deploy--stack-CLI-000000?style=flat&logo=amazon-aws&logoColor=white)](https://github.com/anton-codes-iac/deploy-stack)

## 🌟 The Magic

This repository does **not** rely on manual Terraform scripting, AWS console clicks, or tedious Dockerfile configuration. 

The AWS architecture, zero-CVE Docker configurations, and GitHub Actions CI/CD pipelines were automatically provisioned using the `nest-deploy-stack` integration. The schematic seamlessly patches the NestJS AST (abstract syntax tree) to ensure Docker compatibility, and then silently executes `deploy-stack` to generate the `terraform/` and `.github/` directories natively.

## 🏗️ Architecture Features

* **Serverless Compute:** AWS ECS Fargate container running a highly optimized, unprivileged Node.js environment.
* **Intelligent Code Patching:** Automated modifications to `src/main.ts` to ensure the NestJS app binds to `0.0.0.0` for AWS traffic routing.
* **Managed Database:** Securely attached Amazon RDS PostgreSQL instance running inside a private subnet.
* **Traffic Routing:** Application Load Balancer (ALB) handling health checks and traffic distribution.
* **Zero-Secret CI/CD:** GitHub Actions configured with AWS IAM OIDC (no long-lived access keys).
* **DevSecOps Built-in:** Automated container and infrastructure vulnerability scanning via Trivy on every push.

## 🚀 Try It Yourself

Want to bootstrap and deploy your own production-ready NestJS app to AWS in under 5 minutes?

1. Scaffold a standard NestJS application:
   ```bash
   npx @nestjs/cli new my-nest-app
   cd my-nest-app
   ```
2. Generate the AWS Infrastructure using the schematic:
   ```bash
   npx @nestjs/cli generate nest-deploy-stack --collection nest-deploy-stack
   ```
3. Run the deployment command to provision the real infrastructure in your AWS account:
   ```bash
   npx --yes deploy-stack apply
   ```
4. If you enabled a database, push your local API secrets to the newly created AWS Vault:
   ```bash
   npx --yes deploy-stack secrets push .env
   ```

## 🛑 Safe Teardown

To destroy the AWS infrastructure provisioned by this example (including the RDS database) and stop all billing, run:
```bash
npx --yes deploy-stack destroy
```

## 💰 AWS Costs & Disclaimer
**This tool provisions real AWS resources which will incur charges on your AWS bill.** An ECS Fargate cluster with an Application Load Balancer running 24/7 typically costs around ~$15 - $20/month minimum, depending on your region. A managed RDS database will add additional monthly costs.

*Disclaimer: The maintainers are not responsible for unexpected AWS charges. Always monitor your AWS Billing Dashboard.*
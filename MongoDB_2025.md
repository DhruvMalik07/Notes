# MongoDB Notes 2025

## MongoDB Compass vs MongoDB Atlas

| Feature/Aspect | MongoDB Compass | MongoDB Atlas |
|----------------|-----------------|---------------|
| Type | Desktop GUI tool | Cloud platform (DBaaS) |
| Usage | Connects to local or remote MongoDB instances | Hosts MongoDB databases on cloud (AWS, GCP, Azure) |
| Purpose | Visualize, query, and analyze your data | Create, deploy, scale, and manage MongoDB clusters |
| Installation | Needs to be installed on your system | Accessed via web browser |
| Internet Required? | No (for local DBs) / Yes (for remote DBs) | Yes, since it's cloud-based |
| Best For | Local development, testing, debugging | Production apps, cloud deployments, backups, scaling |
| Security | Depends on your machine/network | Offers built-in cloud security, IP whitelisting, etc. |
| Backup & Monitoring | Manual | Automated backups, monitoring, alerts available |
| Can Connect to Each Other? | Yes – Compass can connect to your Atlas clusters | Yes – Use Compass as a UI for Atlas DBs |

## MongoDB URI

**MongoDB URI (Uniform Resource Identifier)** is a connection string that specifies how our application/tool should connect to MongoDB database.

**Example:**
```
mongodb+srv://<username>:<password>@<cluster-url>/<database>?<options>
```

## CRUD Operations

| Operation | HTTP Method | MongoDB Method | Example Use Case |
|-----------|-------------|----------------|------------------|
| **Create** | `POST` | `insertOne`, `insertMany` | Add a new user or post to the database |
| **Read** | `GET` | `find`, `findOne` | Fetch a user's profile or all blog posts |
| **Update** | `PUT` or `PATCH` | `updateOne`, `updateMany` | Edit a user's profile or change a task status |
| **Delete** | `DELETE` | `deleteOne`, `deleteMany` | Remove a user or delete a product | 
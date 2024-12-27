In MongoDB, **user management** involves creating, managing, and securing user accounts to control access to various databases and collections. MongoDB provides a role-based access control (RBAC) system to ensure that users can only access and modify data based on their assigned roles.

Here's an overview of **MongoDB user management**, including commands for creating users, assigning roles, and performing administrative tasks related to users:

---

### **1. Creating a User**

To create a user in MongoDB, you can use the `createUser()` command. This command allows you to specify the username, password, and roles that the user should have.

#### **Basic Syntax**
```javascript
db.createUser({
  user: "<username>",
  pwd: "<password>",
  roles: [ { role: "<role>", db: "<database>" } ]
});
```

- **user**: The username of the user.
- **pwd**: The password of the user.
- **roles**: A list of roles assigned to the user, specifying what permissions the user has.

#### **Example**: Creating a User with `readWrite` Role
```javascript
use myDatabase;
db.createUser({
  user: "myUser",
  pwd: "myPassword123",
  roles: [ { role: "readWrite", db: "myDatabase" } ]
});
```
This creates a user named `myUser` with the password `myPassword123` and grants them the `readWrite` role on the `myDatabase` database.

---

### **2. Listing Users**

You can list all users in the current database using the `getUsers()` method.

```javascript
db.getUsers();
```

To view the users of a specific database, use the `use <database>` command and then run `db.getUsers()`.

---

### **3. User Roles in MongoDB**

MongoDB comes with several built-in roles that define specific privileges for users. These roles include, but are not limited to:

- **read**: Grants read-only access to all collections in a database.
- **readWrite**: Grants read and write access to all collections in a database.
- **dbAdmin**: Grants administrative privileges to manage the database schema and collections.
- **userAdmin**: Grants privileges to manage users and roles.
- **clusterAdmin**: Grants administrative privileges for managing a MongoDB sharded cluster.
- **root**: Grants superuser privileges, which allow the user to perform all actions in the MongoDB instance.

#### **Common Roles**
- `readWrite`: Read and write access to a database.
- `read`: Read-only access to a database.
- `dbAdmin`: Administrative role for managing indexes, collections, and databases.
- `userAdmin`: Privileges to manage users and roles in a database.
- `clusterAdmin`: Administrative access to manage sharded clusters.
- `root`: Full administrative access for all databases and MongoDB actions.

---

### **4. Updating a User**

To modify an existing user's password or roles, you can use the `updateUser()` method.

#### **Basic Syntax**
```javascript
db.updateUser("<username>", {
  pwd: "<new_password>",  // Optional: Update the password
  roles: [ { role: "<role>", db: "<database>" } ]  // Optional: Assign new roles
});
```

#### **Example**: Updating a User’s Roles
```javascript
use myDatabase;
db.updateUser("myUser", {
  roles: [ { role: "dbAdmin", db: "myDatabase" } ]
});
```
This command updates the `myUser`'s roles to include `dbAdmin` on the `myDatabase` database.

---

### **5. Dropping a User**

If you need to delete a user, you can use the `dropUser()` command.

#### **Syntax**
```javascript
db.dropUser("<username>");
```

#### **Example**: Dropping a User
```javascript
use myDatabase;
db.dropUser("myUser");
```
This removes the user `myUser` from the `myDatabase` database.

---

### **6. Enabling Authentication**

By default, MongoDB does not require authentication, meaning any user can access and perform operations on the databases. To enable authentication, you need to start MongoDB with authentication enabled (`--auth` flag).

- **Start MongoDB with authentication enabled**:
  ```bash
  mongod --auth --port 27017
  ```

Once authentication is enabled, users need to provide a valid username and password to access the database.

---

### **7. Admin User Creation**

To perform administrative tasks like creating users or managing roles, you'll need to create an **admin user** with elevated privileges (e.g., `root` or `userAdminAnyDatabase` role).

#### **Example**: Creating an Admin User
```javascript
use admin;
db.createUser({
  user: "adminUser",
  pwd: "adminPassword123",
  roles: [
    { role: "root", db: "admin" }
  ]
});
```

This creates an `adminUser` with `root` privileges, allowing full access to the MongoDB server.

---

### **8. Granting Roles to Users**

To grant roles to an existing user, you can use the `updateUser()` command, specifying the new roles.

#### **Example**: Granting `userAdmin` Role to a User
```javascript
use myDatabase;
db.updateUser("myUser", {
  roles: [
    { role: "userAdmin", db: "myDatabase" }
  ]
});
```
This grants the `myUser` user the `userAdmin` role in the `myDatabase` database.

---

### **9. Checking User Roles**

To check the roles of a specific user, you can run the `getUser()` method.

```javascript
db.getUser("<username>");
```

#### **Example**: Checking Roles of `myUser`
```javascript
use myDatabase;
db.getUser("myUser");
```
This will show the roles assigned to `myUser` in the `myDatabase` database.

---

### **10. Role Management**

MongoDB allows you to create custom roles for users, which specify a set of privileges. You can use the `createRole()` and `grantRolesToUser()` methods to manage custom roles.

#### **Creating a Custom Role**
```javascript
db.createRole({
  role: "myCustomRole",
  privileges: [
    {
      resource: { db: "myDatabase", collection: "" },
      actions: [ "find", "insert" ]
    }
  ],
  roles: []
});
```
This creates a custom role `myCustomRole` that allows the `find` and `insert` actions on all collections in the `myDatabase` database.

#### **Granting a Custom Role to a User**
```javascript
db.grantRolesToUser("myUser", [ { role: "myCustomRole", db: "myDatabase" } ]);
```

---

### **11. MongoDB Built-In Roles**

Here are some common built-in roles in MongoDB:

- **`read`**: Grants read-only access to all collections in a database.
- **`readWrite`**: Grants read and write access to all collections in a database.
- **`dbAdmin`**: Grants administrative access to database management functions like creating and dropping collections, managing indexes, and more.
- **`userAdmin`**: Grants the ability to create and manage users and roles for a specific database.
- **`root`**: Superuser role, grants all privileges on all databases.
- **`clusterAdmin`**: Provides admin access to manage MongoDB clusters (sharding, replication, etc.).

---

### **12. Authentication Mechanisms**

MongoDB supports different authentication mechanisms, including:

- **SCRAM (Salted Challenge Response Authentication Mechanism)**: Default authentication mechanism in MongoDB.
- **x.509 certificates**: Used for authenticating clients with SSL certificates.
- **LDAP**: Integrates with external LDAP directories for user authentication.

To specify the authentication mechanism when starting the MongoDB server:
```bash
mongod --auth --authenticationMechanisms SCRAM-SHA-1
```

---

### Conclusion

MongoDB's **user management** system is crucial for controlling access to databases and collections, as well as ensuring the security and integrity of your data. By using **roles** and **permissions**, you can easily manage who has access to your MongoDB server and what operations they can perform. Whether you're creating users, updating their roles, or managing authentication, MongoDB provides powerful tools for maintaining secure database environments.
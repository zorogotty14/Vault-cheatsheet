# Vault Cheatsheet (HashiCorp Vault for Secrets Management)

## **Vault Overview**
HashiCorp Vault is a tool for securely managing secrets, tokens, passwords, and encryption keys.

---

## **Vault Installation & Setup**
```sh
vault --version               # Check Vault version
vault server -dev             # Start Vault in development mode
export VAULT_ADDR='http://127.0.0.1:8200'  # Set Vault address
vault status                  # Check Vault server status
```

---

## **Initializing & Unsealing Vault**
```sh
vault operator init           # Initialize Vault (generates unseal keys and root token)
vault operator unseal <key>   # Unseal Vault (repeat with 3 different keys)
vault login <root-token>      # Log in with the root token
```

---

## **Secrets Management**

### **Enable a Secrets Engine**
```sh
vault secrets enable kv       # Enable KV (Key-Value) secrets engine
```

### **Store and Retrieve Secrets**
```sh
vault kv put kv/my-secret password=supersecret  # Store a secret
vault kv get kv/my-secret                        # Retrieve a secret
vault kv delete kv/my-secret                     # Delete a secret
```

---

## **Authentication Methods**
```sh
vault auth list               # List enabled authentication methods
vault auth enable userpass    # Enable username-password authentication
vault write auth/userpass/users/myuser password=mypassword  # Create a user
vault login -method=userpass username=myuser password=mypassword  # Login as a user
```

---

## **Policies & Access Control**

### **Create a Policy**
```sh
vault policy write mypolicy - <<EOF
path "kv/*" {
  capabilities = ["read", "list"]
}
EOF
```

### **Assign a Policy to a User**
```sh
vault write auth/userpass/users/myuser policies=mypolicy
```

---

## **Token Management**
```sh
vault token create            # Create a new token
vault token lookup <token>    # Look up details of a token
vault token revoke <token>    # Revoke a token
```

---

## **Audit Logs**
```sh
vault audit enable file file_path=/var/log/vault_audit.log  # Enable audit logs
vault audit disable file  # Disable audit logs
```

---

## **Useful Vault Resources**
- [Vault Documentation](https://developer.hashicorp.com/vault/docs)
- [Vault Commands Reference](https://developer.hashicorp.com/vault/docs/commands)
- [Vault Best Practices](https://developer.hashicorp.com/vault/tutorials)

---

This cheatsheet provides a quick reference for Vault setup, secrets management, authentication, and policies. Let me know if you need any modifications!


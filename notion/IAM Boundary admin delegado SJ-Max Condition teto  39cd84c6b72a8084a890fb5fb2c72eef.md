# IAM Boundary | admin delegado | SJ-Max | Condition | teto de permissões

joao = 1 politica permitindo criare       | SJ-DelegatedAdmin

poltica 2 (maxima) nao no joao, MAS sempre a role que joao criar vai com essa      | SJ-MAX

SJ-DelegatedAdmin (JOAO)

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "RoleCreationWithPermission",
            "Effect": "Allow",
            "Action": ["iam:CreateRole", "iam:AttachRolePolicy", "iam:PutRolePolicy",
                       "iam:DetachRolePolicy", "iam:DeleteRolePolicy"],
            "Resource": "*",
            "Condition": {
                "StringEquals": { "iam:PermissionsBoundary": "arn:aws:iam::12345:policy/SJ-Max" }
            }
        },
        {
            "Sid": "IAMPermission",
            "Effect": "Allow",
            "Action": ["iam:CreatePolicy", "iam:GetRole", "iam:ListRoles",
                       "iam:DeletePolicy", "iam:DeleteRole", "iam:GetRolePolicy"],
            "Resource": "*"
        }
    ]
}
```

SJ-MAX = (Police fora de Joao)

```jsx
{
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": ["ssm:PutParameter", "s3:*"],  #servicos maximos 
        "Resource": "*"
    }]
}
```
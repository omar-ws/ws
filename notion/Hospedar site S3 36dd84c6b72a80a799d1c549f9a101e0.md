# Hospedar site S3

politica baseada em recurso:

```jsx
{
"Version": "2012-10-17",
"Statement": [
{
"Sid": "Statement1",
"Effect": "Allow",
"Principal": "*",
"Action": "s3:GetObject",
"Resource": "arn:aws:s3:::redacaoparana1-342946498914-us-east-1-an/*"
}
]
}
```
# Load Balancer

Target Group, sao agrupamentos logicos de EC2, ECS, nada mais que isso nao estao necessariamente involvidas com AZ

```jsx
No CloudFront você adiciona o header na Origin Request Policy / Política de requisição de origem:
- Origin → Edit → Add custom header
- Header: X-Origin-Verify
- Value: valor-secreto
```

senha: a3f8c2d1-9b4e-4f7a-8c3d-2e1f9a0b5c6d

http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/add-origin-custom-headers.html 

![image.png](image%2047.png)

![image.png](image%2048.png)
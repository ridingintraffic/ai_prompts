prompt:  
```i want an aws iam policy document in json, that allows codeartifact to be shared across an aws org based on the org id ```

iam_policy
```{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowCodeArtifactAccessFromOrg",
            "Effect": "Allow",
            "Action": [
                "codeartifact:GetRepositoryEndpoint",
                "codeartifact:ReadFromRepository",
                "codeartifact:GetPackageVersionReadme",
                "codeartifact:GetRepositoryPermissionsPolicy",
                "codeartifact:List*",
                "codeartifact:Describe*"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalOrgID": "o-exampleorgid"
                }
            }
        }
    ]
}
```
domain_policy  
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowCodeArtifactDomainAccessFromOrg",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "codeartifact:DescribeDomain",
                "codeartifact:DescribeRepository",
                "codeartifact:ListRepositoriesInDomain",
                "codeartifact:GetRepositoryEndpoint",
                "codeartifact:GetAuthorizationToken",
                "codeartifact:ReadFromRepository",
                "codeartifact:GetPackageVersionReadme"
            ],
            "Resource": "arn:aws:codeartifact:region:account-id:domain/domain-name",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalOrgID": "o-exampleorgid"
                }
            }
        }
    ]
}
```
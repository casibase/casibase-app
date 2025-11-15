# WeChat Verification File

## For WeChat Mini Program Business Domain Verification

When you configure your domain as a Business Domain (业务域名) in the WeChat Mini Program Admin Console, you will need to download a verification file.

### Steps:

1. Log in to [WeChat MP Console](https://mp.weixin.qq.com/)
2. Navigate to: Development → Development Settings → Business Domain
3. Add your domain (e.g., `mini.casibase.com`)
4. Download the verification file (usually named like `WxVerifyFile.txt`)
5. Upload this file to the **root directory** of your web server

### Important Notes:

- The verification file must be accessible at: `https://yourdomain.com/WxVerifyFile.txt`
- The file must return HTTP 200 status
- The file must be served over HTTPS
- Do NOT modify the content of the verification file
- The file name is case-sensitive

### This is NOT the WeChat app verification

This verification is for the **H5 website** that is embedded in the mini program's `web-view`, not for the mini program itself.

The verification file should be placed on the server hosting the Casibase H5 interface (e.g., `mini.casibase.com`), not in this app repository.

## Example

If your Casibase URL is `https://mini.casibase.com/`, then the verification file should be accessible at:
```
https://mini.casibase.com/WxVerifyFile.txt
```

## Troubleshooting

If verification fails:
- Check if the file is accessible in a browser
- Verify HTTPS certificate is valid
- Ensure no redirects are happening
- Check file permissions on the server
- Make sure the domain matches exactly (including www or non-www)

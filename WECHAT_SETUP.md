# WeChat Mini Program Setup Guide

This guide will help you fix the "Failed to load page" blank screen issue in the WeChat mini program.

## Issue: Blank Screen with Network Error

When the WeChat mini program shows a blank screen with the error "Failed to load page. Please check your network connection and try again", it's typically because the domain is not properly configured in WeChat's backend.

## Solution

### 1. Configure Business Domain (业务域名)

The `web-view` component in WeChat mini programs requires the embedded domain to be registered as a "Business Domain" in the WeChat Mini Program Admin Console.

**Steps:**

1. Log in to [WeChat Mini Program Admin Console](https://mp.weixin.qq.com/)
2. Navigate to: **Development** → **Development Management** → **Development Settings** → **Business Domain**
3. Click **Add** and enter your domain (e.g., `mini.casibase.com`)
4. Download the verification file (e.g., `WxVerifyFile.txt`)
5. Upload the verification file to the root directory of your domain server
   - The file must be accessible at: `https://mini.casibase.com/WxVerifyFile.txt`
6. Click **Verify** in the WeChat console

### 2. Configure Server Domain (服务器域名)

In addition to the Business Domain, you should also configure the Server Domain for API requests:

1. In the same **Development Settings** page, find **Server Domain**
2. Add your domain to:
   - **request合法域名** (Request domain)
   - **downloadFile合法域名** (Download domain) - if needed
   - **uploadFile合法域名** (Upload domain) - if needed

### 3. HTTPS Requirement

⚠️ **Important**: All domains must use HTTPS with a valid SSL certificate issued by a trusted CA.

### 4. Testing

After configuration:
1. Wait 5-10 minutes for changes to take effect
2. Rebuild your mini program: `npm run build:mp-weixin`
3. Open the mini program in WeChat Developer Tools
4. Test the web-view loading

### 5. Development vs Production

- **Development**: Set `"urlCheck": false` in `src/manifest.json` → `mp-weixin.setting` to bypass domain checks during development
- **Production**: Always configure domains properly and set `"urlCheck": true`

## Common Issues

### Issue: "Cannot verify domain"
**Solution**: Ensure the verification file is accessible via HTTPS and returns a 200 status code.

### Issue: "Web-view still shows blank screen after configuration"
**Solution**: 
- Clear cache in WeChat Developer Tools
- Verify the domain uses HTTPS
- Check if the H5 page loads correctly in a regular browser
- Ensure no redirects that change the domain

### Issue: "Page loads but functions don't work"
**Solution**: Check that all API endpoints used by the H5 page are also whitelisted in Server Domains.

## Configuration Checklist

- [ ] Added domain to Business Domain in WeChat MP Console
- [ ] Uploaded verification file to domain root
- [ ] Verified domain in WeChat MP Console
- [ ] Added domain to Server Domain (if making API calls)
- [ ] Ensured domain uses valid HTTPS
- [ ] Tested in WeChat Developer Tools
- [ ] Tested in actual WeChat app

## Reference

- [WeChat Mini Program web-view Component Documentation](https://developers.weixin.qq.com/miniprogram/dev/component/web-view.html)
- [WeChat Mini Program Domain Configuration](https://developers.weixin.qq.com/miniprogram/dev/framework/ability/network.html)

# Description
Create a sight level data variable to carry the check for the cookie policy check

Use: 
{{#if @accpetedCookiePolicy}}
    <div>show this when cookie policy has been accepted</div>
{{else}}
    <div>show this otherwise</div>
{{/if}}

# Some what related
https://dotnetfalcon.com/create-custom-helpers-to-add-functionality-to-your-ghost-blog/ 

# Wiring up acceptedCookiePolicy
## In Ghost Source Tree
core\frontend\services\themes\middleware.js

    var cookies = req.headers.cookie ? req.headers.cookie : "";
    hbs.updateTemplateOptions({
        data: {
            blog: siteData,
            site: siteData,
            accpetedCookiePolicy: Boolean(cookies.toString().indexOf("wpcc=dismis") >= 0),
            labs: labsData,
            config: themeData,
            price: priceData
        }
    });

## In Ghost Setting - Code Injection

    if(document.cookie.toString().indexOf('wpcc=dismis') < 0) 
    { 
        myChecker = setInterval(function() 
        {
            console.log('yep'); 
            if(document.cookie) 
            {
                if(document.cookie.toString().indexOf('wpcc=dismis') >=0) 
                {
                    clearInterval(myChecker); 
                    alert('Thank you for accepting the cookie policy. About to refresh.'); 
                    window.location.reload();
                }
            }
        }, 1000);
    }


# Domain Fronting For Fastly

**Author:** DoctorEww

**Working As of Date (WAD):** 06/24/20

**CDN Organization:** Fastly

## Conditions To meet

In order to front the given domain, the following conditions must be met for
success:

- Target Domain must exist on Fastly CDN
- Your fronted domain must exist on Fastly CDN
- Both domains must use HTTPS

## Execution Steps

**Fronted Domain:** The allowed domain you are using as a "mask".

**Target Domain:** The domain you want to access, using the Fronted domain.

1. Follow the steps to setup a resource on
   [Fastly CDN](https://www.fastly.com/products/cdn)

   1. A account can be made for free. "Free Trial" gives \$50 credit.

2. Construct your HTTPS request with the target domain in the `Host:` header and
   the fronted domain as the primary domain you wish to access. The following
   two methods are just two ways to do it:

   1. **cURL:**

      ```bash
      curl -H "Host: <Target_domain>" https://<Fronted_domain>
      ```

   2. **Python:**

      ```python
      import urllib.request as request

      TARGET = 'target_domain'
      FRONTED = 'https://domain.to.front'
      h = {}
      h['Host'] = TARGET
      h['User-Agent'] = "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.1916.47 Safari/537.36"
      req = request.Request(
          FRONTED,
          data=None,
          headers=h
          )
      response = request.urlopen(req, timeout=60)

      # Check if we fronted or not, if so, print data
      if response.code == 200:
          for line in response.readlines():
              print(line.decode())
      else:
          print("Failed to front.")
      ```

## Potential Issues and Errors

- Fastly has worked on every
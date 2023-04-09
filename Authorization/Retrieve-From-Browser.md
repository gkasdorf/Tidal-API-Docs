# Retrieving `access_token` from the browser
1. Visit [Tidal's Web Player](https://listen.tidal.com/) and sign in.
2. Open the developer tools inside your browser.
3. Select the `Network` tab.
4. Look for `Fetch/XHR` requests. Select one.
5. View the `Headers` tab and copy the value of the `authorization` field.

Note that this token will expire **in one day**. If you wish to find the `refresh_token`, we will cover that below.

## Retrieving the `refresh_token`
The easiest way to find the `refresh_token` is to follow these steps:

1. Visit [Tidal's Web Player](https://listen.tidal.com/). Sign out if you are already signed in.
2. Before doing anything else, open your browsers developer tools and go to the `Network` tab.
3. Perform the authentication process.
4. Once you have been redirected back to the web player, enter `/auth/token` in the search box under network. You will see a result similar to the picture below.

![picture 1](https://ucf3c2a4274e89cc0ec878851c45.previews.dropboxusercontent.com/p/thumb/AB0hu-fkReUff1w14INCEi4_hxxGvn9aSQW5HU9rDeMh5QD6DpIuZ3dH9AzUREj_3D_ERaCG58v5EYdYyo6upDP9rCzMjJ6o-8Hdkxe9_e8zBSrXhdUUGWhhI91xdfWAY5GgBQ7JK0c5cXXwrKlz3vd8sMBBYHQvKSYlvMSMqFXbRU8VCYi1Eya33vfrcsArcgfUmtRqec2lkQOlsnD_Nh9xLoyTIhZjZEnYfn1sbiD1CpgFEQ7B2SzFYOo61BqyB1Q6xGiRH9Yf3PgUrAk9X9xOyCJarfUJ-IGEbNec2QGvahqA7tm7wHnccEono0t5oMWFzEkiEEe3kDJ7NvRDG_GC29J7J9xSpcT4vSLG8tRh9AVvaQkD0P_HTRUZl3kiLxzVgv0KPNYDbhiG7lFQ3iW-/p.png)

5. Select `token`, then select `Preview`. You will find the `access_token` and `refresh_token` here.

![picture 2](https://uc1bb041864f82ca5d327c67b615.previews.dropboxusercontent.com/p/thumb/AB1yAMFOVr_4ea109Fgul33xFF6nzDS_i8Tn9SgLXG6_g8SsTDgatclruRIciwcVBzjRCECMXLcg6XlvZX4y-gHiKD8G_Jwv-sDT_bwsiQU-DAdOxiUsjMlHMJ6lAjuRYI_jh2DBf6rJtZsGBwpOoR1XIXhJyOcDI1SaH7pO62Py-HGZ85PcSUzj82kCRpBtBPlnI8QqFsSDge4RW5UtdcGRCe-GlcdKwVjl-beXZp8wvTxVx6cr-WazJK0ZlN5X7KTYDi4eU9z64iLpESAi2orUCHszDKmwbERDE_f3YMRYVtMG3Fg_SC2WpUdXOgJNH66t8n1CvvlXIQao06L7Jaa_xGheAQUcGxPlC9V-2W0sr4DCb5hkLtaSf8Sg6JNLLFaXgVfOpqnIzPLZynF4b7AV/p.png)

## Ensuring that the credentials are not destroyed
If you choose to sign out of the web player for any reason, these credentials will be destroyed. It is advisable that you simply delete all the application data from the browser after you have recorded your credentials. That way, you can continue to use these credentials in your application and still log in and out of the Tidal web player.

![picture 3](https://uc1528e89c6c38a1937d7f791662.previews.dropboxusercontent.com/p/thumb/AB0O6zdP1o97wUVJYCrdTHin_SepbgqOkIqmOqg7vDqhxMgjJ58rtlHvvZMAfVFBiMn5m3uOkNBLim0UWxPyQyTATt-tC89_xKZWvE5J057y5Z2rknob0UMWPcoEWwdJttB62v0aYhVDXxE7uMi237eO81ajkY04Rml53orSmlRdlD_3DSe_FLRpYSIenK_zLEX-cOFIG7tN9squ9ZcgT8_PF0YCmVEwCeLOk0tWITydCZ3rbyEE3GcQ62fGNcTKZ0ngNJvomMpwN1POheVf7-bFaiGRqeF9gBmj8-2DzQLg89ofHZ8WdPN_kVEDIjanQB61PU5fxuddbE7-6wVtxUJtcDYEAFtnvU1W9CJ42hRs9x6jjVFbKC9x8fwzAKMwSoY4Ok6b1QvDAZNrE-Rhjq2z/p.png)

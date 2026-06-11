# DNS dla kwiaciarniafloria.pl — instrukcja (Cloudflare)

> Plik roboczy dla Michała — nie wpływa na stronę. Po wykonaniu można usunąć.

## Kolejność

1. **OVH:** zarejestruj `kwiaciarniafloria.pl` (dokładnie ta nazwa — jest w canonical/schema). Włącz 2FA na koncie OVH.
2. **Cloudflare:** Add site → kwiaciarniafloria.pl → plan Free → Cloudflare pokaże 2 nameservery.
3. **OVH:** panel domeny → Serwery DNS → podmień na te z Cloudflare. Propagacja: do kilku godzin.
4. **Cloudflare Pages:** Workers & Pages → Create → Pages → połącz repo GitHub `mazurekdeveloper/Floria` → build: brak (statyczna), output: `/` → Deploy → Custom domains → dodaj kwiaciarniafloria.pl i www.
   - Plik `_headers` (już w repo) ustawi nagłówki bezpieczeństwa automatycznie.
5. **SSL/TLS** (zakładka w Cloudflare): tryb **Full (strict)**. Edge Certificates → włącz "Always Use HTTPS".

## E-mail: kontakt@kwiaciarniafloria.pl (0 zł)

6. Cloudflare → Email → Email Routing → Enable → utwórz adres `kontakt@` → cel: prywatna skrzynka klientki → klientka klika link potwierdzający.
   - Cloudflare sam doda rekordy MX i SPF — zaakceptuj proponowane.

## Antyspoofing (żeby nikt nie podszył się pod kwiaciarnię)

7. Cloudflare → DNS → dodaj rekord TXT:
   - Nazwa: `_dmarc` | Treść: `v=DMARC1; p=reject; rua=mailto:mimazurek07@gmail.com`
   - (SPF doda Email Routing; jeśli routing nieużywany, dodaj TXT `@`: `v=spf1 -all`)

## Po wdrożeniu — weryfikacja (5 min)

- https://securityheaders.com → wpisz domenę → cel: ocena A/A+
- https://pagespeed.web.dev → mobile > 90
- Google Search Console → dodaj domenę, wyślij sitemap.xml
- Google Business Profile klientki → wpisz adres strony

## Roczny koszt utrzymania

Domena ~62 zł/rok (OVH, odnowienie). Hosting, SSL, e-mail, ochrona DDoS: 0 zł. Przychód: 140 zł/mies. = 1680 zł/rok. Marża ~96%.

# Introduzione

L'autenticazione Server-Side in Blazor di default è implementata via cookies.

Attraverso una semplice pagina Razor è possibile richiedere username e password ed effettuarne la verifica.

Nel metodo **OnPost** è possibile effettuare le verifiche del caso, ad esempio validando le informazioni attraverso i dati presenti in un DB, ed effettuare una chiamata al sistema di autenticazione base `Microsoft.AspNetCore.Authentication`.

Esempio di codice:

```c#
var claims = new List<Claim>
{
    new Claim(ClaimTypes.Name, "Nicola"),
    new Claim(ClaimTypes.Email, "nic@email.com")
};

var claimsIdentity = new ClaimIdentity(
	claims,
    CookieAuthenticationDefaults.AuthenticationScheme
);

await HttpContext.SignInAsync(
	CookieAuthenticationDefaults.AuthenticationScheme,
	new ClaimsPrincipal(claimsIdentity));

```

Nell'esempio di codice sopra riportato la costante `CookieAuthenticationDefaults.AuthenticationScheme` contiene "Cookies".

### Logout

Allo stesso modo per effettuare il _Logout_ è sufficiente creare un'ulteriore pagina Razor e aggiungere al metodo **OnGet** il seguente codice:

```csharp
await HttpContext.SignOutAsync(CookieAuthenticationDefaults.AuthenticationScheme);
```

Al termine di questa operazione il cookie denominato **.AspNetCore.Cookies** verrà rimosso dalla collection Cookies del browser.


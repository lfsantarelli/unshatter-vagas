# unshatter-vagas

Disponibilidade de ingressos do filme **LINKIN PARK: UNSHATTER** nos cinemas
brasileiros, em JSON, para alimentar painéis públicos.

- **Arquivo:** [`dados.json`](https://raw.githubusercontent.com/lfsantarelli/unshatter-vagas/main/dados.json)
- **Fonte:** API pública da ingresso.com. Os lugares são contados um a um no mapa de
  assentos de cada sessão. `cap` é só o que está à venda — lugares bloqueados por
  distanciamento ficam de fora.
- **Atualização:** automática, a cada 10 minutos.

## Formato

```jsonc
{
  "medido": "2026-08-12T15:39-03:00",   // quando a medição rodou
  "medido_br": "12/08/2026 às 15h39",
  "fonte": "ingresso.com",
  "sessoes": [
    {
      "uf": "SP", "cid": "São Paulo", "cin": "Kinoplex Vila Olímpia",
      "sala": "Sala 2", "h": "20:30", "t": "Normal/Legendado", "p": 68.39,
      "liv": 14,        // lugares livres
      "ocu": 114,       // ocupados
      "cap": 128,       // capacidade vendável (liv + ocu)
      "pct": 89.1,      // % vendido
      "ok": true,       // false = não foi possível ler o mapa; NÃO é "esgotada"
      "d": "2026-09-30",
      "sid": "86374639" // sessionId: checkout.ingresso.com/assentos?sessionId=…
    }
  ]
}
```

> `ok: false` significa **sem leitura**, não lotação. Quem consome tem de distinguir
> as duas coisas: tratar leitura falha como "esgotada" mostraria o oposto da verdade.

Serve com `access-control-allow-origin: *`, então dá para consumir direto do
navegador, de qualquer domínio.

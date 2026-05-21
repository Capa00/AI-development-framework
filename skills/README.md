# Skills

Questa cartella contiene le skill utilizzate per estendere e specializzare il comportamento degli strumenti AI durante le attività di sviluppo software.

## Convenzioni Anthropic

Le skill presenti in questa cartella devono rispettare le convenzioni definite da [Anthropic Claude Skills Documentation](https://support.claude.com/en/articles/12512198-how-to-create-custom-skills?utm_source=chatgpt.com) e dal repository ufficiale [anthropics/skills](https://github.com/anthropics/skills?utm_source=chatgpt.com). ([Claude Centro Assistenza][1])

In particolare:

* ogni skill dovrebbe essere contenuta in una cartella dedicata;
* ogni skill deve includere un file `SKILL.md`;
* `SKILL.md` dovrebbe contenere:

  * YAML frontmatter;
  * `name`;
  * `description`;
  * istruzioni operative in markdown;
* la `description` deve descrivere chiaramente:

  * cosa fa la skill;
  * quando dovrebbe essere utilizzata;
* eventuali file aggiuntivi dovrebbero essere organizzati in cartelle dedicate come:

  * `references/`
  * `scripts/`
  * `templates/`
  * `assets/`
* le skill dovrebbero essere piccole, focalizzate e componibili;
* evitare skill monolitiche o troppo generiche;
* mantenere `SKILL.md` sintetico e spostare documentazione estesa in file separati;
* utilizzare naming semplice e descrittivo, preferibilmente lowercase con hyphen (`my-skill-name`). ([Claude Centro Assistenza][1])

## Versionamento delle skill

Non è consigliato modificare direttamente le skill già esistenti, soprattutto se sono già utilizzate o referenziate in workflow attivi.

Quando una skill evolve in modo significativo, è preferibile creare una nuova versione mantenendo anche quella precedente.

Convenzione suggerita:

```
<nome_sskill>
<nome_skill>_v2_0
<nome_skill>_v3_0
```

## Relazione con gli esperimenti

Le skill non sono considerate definitive.

Molte skill nascono dagli esperimenti documentati nella cartella `experiments` e possono evolvere nel tempo in base ai risultati osservati, ai rischi identificati e ai feedback raccolti nei progetti reali.

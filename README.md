# arr-custom-formats
Mini guide pour grab et MAJ ses médias dans la version la plus légère, à ajuster pour la qualité souhaitée, avec des formats personnalisés et un profil unique sur Radarr et Sonarr.<br>
<br>

Pour importer les **custom formats** plus bas dans la page, se référer aux **TRaSH Guides** suivant :<br>
<b>Radarr :</b> <a href="https://trash-guides.info/Radarr/Radarr-import-custom-formats/" target="_blank">Créer</a> | <a href="https://trash-guides.info/Radarr/Radarr-how-to-update-custom-formats/" target="_blank">Mettre à jour</a><br>
<b>Sonarr :</b> <a href="https://trash-guides.info/Sonarr/sonarr-import-custom-formats/" target="_blank">Créer</a> | <a href="https://trash-guides.info/Sonarr/sonarr-how-to-update-custom-formats/" target="_blank">Mettre à jour</a>

## Radarr

### Custom Formats

**DV (WEBDL)**<br>
Pour exclure les médias qui indiquent uniquement DV (Dolby Vision), non compatible avec mon matériel ou celui des personnes avec qui je partage ma bibliothèque.<br>
  ```sh
  {
  "name": "DV (WEBDL)",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Dolby Vision",
      "implementation": "ReleaseTitleSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "value": "\\b(dv|dovi|dolby[ .]?vision)\\b"
      }
    },
    {
      "name": "WEBDL",
      "implementation": "SourceSpecification",
      "negate": false,
      "required": false,
      "fields": {
        "value": 7
      }
    },
    {
      "name": "WEBRIP",
      "implementation": "SourceSpecification",
      "negate": false,
      "required": false,
      "fields": {
        "value": 8
      }
    },
    {
      "name": "Not RlsGrp",
      "implementation": "ReleaseGroupSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": "\\b(Flights)\\b"
      }
    },
    {
      "name": "Not HDR",
      "implementation": "ReleaseTitleSpecification",
      "negate": true,
      "required": true,
      "fields": {
        "value": "\\bHDR(\\b|\\d)"
      }
    },
    {
      "name": "Not Hulu",
      "implementation": "ReleaseTitleSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": "\\b(hulu)\\b"
      }
    }
  ]
}
  ```
<br>
<br>

**DV + HDR**<br>
Permet d'inclure les médias qui sont HDR compatible malgré le DV, ça évite d'exclure trop de sources alors qu'elles sont lues par tout matériel assez récent<br>
  ```sh
  {
  "name": "DV + HDR",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Dolby Vision",
      "implementation": "ReleaseTitleSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "value": "\\b(dv|dovi|dolby[ .]?vision)\\b"
      }
    },
    {
      "name": "WEBDL",
      "implementation": "SourceSpecification",
      "negate": false,
      "required": false,
      "fields": {
        "value": 7
      }
    },
    {
      "name": "WEBRIP",
      "implementation": "SourceSpecification",
      "negate": false,
      "required": false,
      "fields": {
        "value": 8
      }
    },
    {
      "name": "Not RlsGrp",
      "implementation": "ReleaseGroupSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": "\\b(Flights)\\b"
      }
    },
    {
      "name": "HDR",
      "implementation": "ReleaseTitleSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "value": "\\bHDR(\\b|\\d)"
      }
    },
    {
      "name": "Not Hulu",
      "implementation": "ReleaseTitleSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": "\\b(hulu)\\b"
      }
    }
  ]
}
  ```
<br>
<br>

**FR**<br>
Afin de reconnaître si un média est uniquement avec une piste son française (true french, etc..)<br>
  ```sh
  {
  "name": "FR",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Langue",
      "implementation": "LanguageSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "value": 2,
        "exceptLanguage": false
      }
    },
    {
      "name": "480p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 480
      }
    },
    {
      "name": "720p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 720
      }
    },
    {
      "name": "exclu",
      "implementation": "ReleaseTitleSpecification",
      "negate": true,
      "required": true,
      "fields": {
        "value": "\\bMULTI(?:[ ._-]?(?:VFI|VFF|VFQ|VF2|VFF2|VFI2|\\d))?\\b|\\b(vfq|vfi|vq)\\b|\\bFR\\s*\\+\\s*[A-Z]{2}\\b|\\b[A-Z]{2}\\s*\\+\\s*FR\\b"
      }
    },
    {
      "name": "Title FR",
      "implementation": "ReleaseTitleSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "value": "\\b(vf|truefr|french|francais|français|vof|VFF|VF2|VFF2)\\b"
      }
    }
  ]
}
  ```
<br>
<br>

**FRQ**<br>
Piste son en québecois, tabarnak !<br>
  ```sh
  {
  "name": "FRQ",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Langue",
      "implementation": "LanguageSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "value": 2,
        "exceptLanguage": false
      }
    },
    {
      "name": "480p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 480
      }
    },
    {
      "name": "720p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 720
      }
    },
    {
      "name": "exclu",
      "implementation": "ReleaseTitleSpecification",
      "negate": true,
      "required": true,
      "fields": {
        "value": "\\bMULTI(?:[ ._-]?(?:VFI|VFF|VFQ|VF2|VFF2|VFI2|\\d))?\\b|\\b(vf|vff|truefr|french|vof)\\b|\\bFR\\s*\\+\\s*[A-Z]{2}\\b|\\b[A-Z]{2}\\s*\\+\\s*FR\\b"
      }
    },
    {
      "name": "Title FRQ",
      "implementation": "ReleaseTitleSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "value": "\\b(vfq|vfi|vq)\\b"
      }
    }
  ]
}
  ```
<br>
<br>

**Max 2Go**<br>
Pour forcer le grab ou la MAJ vers un média en-dessous de 2Go (favorise les releases en h265 très légère, à appliquer uniquement si vous voulez économiser de l'espace disque - ce qui est mon cas)<br>
  ```sh
  {
  "name": "Max 2 Go",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "2 Go max",
      "implementation": "SizeSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "min": 0,
        "max": 2
      }
    },
    {
      "name": "480p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 480
      }
    },
    {
      "name": "720p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 720
      }
    }
  ]
}
  ```
<br>
<br>

**Max 3 Go**<br>
Orienter vers des releases de moins de 3Go<br>
  ```sh
  {
  "name": "Max 3 Go",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "3 Go max",
      "implementation": "SizeSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "min": 0,
        "max": 3
      }
    },
    {
      "name": "480p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 480
      }
    },
    {
      "name": "720p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 720
      }
    }
  ]
}
  ```
<br>
<br>

**Max 4Go**<br>
Orienter vers des releases de moins de 4Go<br>
  ```sh
  {
  "name": "Max 4 Go",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "4 Go max",
      "implementation": "SizeSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "min": 0,
        "max": 4
      }
    },
    {
      "name": "480p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 480
      }
    },
    {
      "name": "720p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 720
      }
    }
  ]
}
  ```
<br>
<br>

**Max 6Go**<br>
Orienter vers des releases de moins de 6Go<br>
  ```sh
  {
  "name": "Max 6 Go",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "6 Go max",
      "implementation": "SizeSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "min": 0,
        "max": 6
      }
    },
    {
      "name": "720p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 720
      }
    },
    {
      "name": "480p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 480
      }
    }
  ]
}
  ```
<br>
<br>

**MULTi**<br>
Reconnaître les vraies releases MULTi<br>
  ```sh
  {
  "name": "Multi",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Original",
      "implementation": "LanguageSpecification",
      "negate": false,
      "required": false,
      "fields": {
        "value": -2,
        "exceptLanguage": false
      }
    },
    {
      "name": "French",
      "implementation": "LanguageSpecification",
      "negate": false,
      "required": false,
      "fields": {
        "value": 2,
        "exceptLanguage": false
      }
    },
    {
      "name": "480p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 480
      }
    },
    {
      "name": "720p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 720
      }
    },
    {
      "name": "Title Multi",
      "implementation": "ReleaseTitleSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "value": "(?i)\\bMULTI(?:[ ._-]?(?:VFI|VFF|VFQ|VF2|VFQ2|VFF2|VFI2|\\d))?\\b(?![ ._-]?subs?)|\\bFR\\s*\\+\\s*[A-Z]{2}\\b|\\b[A-Z]{2}\\s*\\+\\s*FR\\b"
      }
    }
  ]
}
  ```
<br>
<br>

**VOST**<br>
Pour reconnaître les releases uniquement en VOSTFR<br>
  ```sh
  {
  "name": "VOST",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "480p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 480
      }
    },
    {
      "name": "720p OUT",
      "implementation": "ResolutionSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 720
      }
    },
    {
      "name": "exclu",
      "implementation": "ReleaseTitleSpecification",
      "negate": true,
      "required": true,
      "fields": {
        "value": "\\bMULTI(?:[ ._-]?(?:VFI|VFF|VFQ|VF2|VFF2|VFI2|\\d))?\\b|\\b(vf|vff|vfq|vfi|truefr|french|vof)\\b|\\bFR\\s*\\+\\s*[A-Z]{2}\\b|\\b[A-Z]{2}\\s*\\+\\s*FR\\b"
      }
    },
    {
      "name": "Title Sous-titres",
      "implementation": "ReleaseTitleSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "value": "\\b(vost|vostfr|subfr|subfrench)\\b"
      }
    },
    {
      "name": "FR",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 2,
        "exceptLanguage": false
      }
    }
  ]
}
  ```
<br>
<br>
<br>

### Profils

Voici un exemple des scores que j'ai appliqué uniquement sur HD-1080p, à adapter à ce que vous souhaitez :)<br>
<br>
<img src="images/score-radarr.jpg" alt="score Radarr" width="100%" height="auto">
<br>
<br>
<br>

## Sonarr

### Custom Formats

**NOM**<br>
Descriptif<br>
  ```sh
  {
  "name": "DV (WEBDL)",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Dolby Vision",
      "implementation": "ReleaseTitleSpecification",
      "negate": false,
      "required": true,
      "fields": {
        "value": "\\b(dv|dovi|dolby[ .]?vision)\\b"
      }
    },
    {
      "name": "WEBDL",
      "implementation": "SourceSpecification",
      "negate": false,
      "required": false,
      "fields": {
        "value": 7
      }
    },
    {
      "name": "WEBRIP",
      "implementation": "SourceSpecification",
      "negate": false,
      "required": false,
      "fields": {
        "value": 8
      }
    },
    {
      "name": "Not RlsGrp",
      "implementation": "ReleaseGroupSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": "\\b(Flights)\\b"
      }
    },
    {
      "name": "Not HDR",
      "implementation": "ReleaseTitleSpecification",
      "negate": true,
      "required": true,
      "fields": {
        "value": "\\bHDR(\\b|\\d)"
      }
    },
    {
      "name": "Not Hulu",
      "implementation": "ReleaseTitleSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": "\\b(hulu)\\b"
      }
    }
  ]
}
  ```
<br>
<br>

**NOM**<br>
Descriptif<br>
  ```sh
  
  ```
<br>
<br>

**NOM**<br>
Descriptif<br>
  ```sh
  
  ```
<br>
<br>

**NOM**<br>
Descriptif<br>
  ```sh
  
  ```
<br>
<br>

**NOM**<br>
Descriptif<br>
  ```sh
  
  ```
<br>
<br>

**NOM**<br>
Descriptif<br>
  ```sh
  
  ```
<br>
<br>

**NOM**<br>
Descriptif<br>
  ```sh
  
  ```
<br>
<br>

**NOM**<br>
Descriptif<br>
  ```sh
  
  ```
<br>
<br>

**NOM**<br>
Descriptif<br>
  ```sh
  
  ```
<br>
<br>

**NOM**<br>
Descriptif<br>
  ```sh
  
  ```
<br>
<br>

**NOM**<br>
Descriptif<br>
  ```sh
  
  ```
<br>
<br>
<br>

### Profils

Voici un exemple des scores que j'ai appliqué uniquement sur HD-1080p, à adapter à ce que vous souhaitez :)<br>
<br>
<img src="images/score-sonarr.jpg" alt="score Sonarr" width="100%" height="auto">
<br>
<br>
Have fun !




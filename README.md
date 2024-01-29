Starry Ocean API Documentation
==============================

* * *

### TABLE OF CONTENTS

* - 1.  Explanation
        - Overview
        - Options
        - Features
* 2. Requirements & Installation
* 3.  Data Type
* 4.  Endpoints
* 5.  Errors

* * *



* * *

## 1. EXPLANATION 

### Overview

Leveraging the Django REST Framework and designed with a class-based view approach, STARRY OCEAN API serves as either a REST API / GUI toward a compendium of Star Ocean (© Square Enix) characters.

The Starry Ocean API allows you to search for characters from the following Star Ocean games:
###### Star Ocean 1
  - `Star Ocean First Departure R` (PS4, Nintendo Switch)
  - `Star Ocean: Fantastic Space Odyssey` (SNES)

###### Star Ocean 2
  - `Star Ocean: The Second Story` (Playstation)
  - `Star Ocean: The Second Story R` (Nintendo Switch, PlayStation 5, PlayStation 4, Microsoft Windows)

### Options
* Install this app for its GUI (as seen on: https://www.matthewsummers.dev/starry-ocean/)
    - Follow this documentation fully
* Don't install this app and just call the hosted API directly to access the data
    - Skip to `4. ENDPOINTS` below

### Features
* The app provides a GUI with a search feature to allow users to search for Star Ocean 1 and 2 characters
    - Provides character descriptions
    - Provides character images
* The app also provides options to display a compilation of each respective series' characters on a one-page display

* Alternatively, forgo the app installation.  Call the host directly:
    - Can be used by external services to access the data

* * * 



* * * 
## 2. REQUIREMENTS & INSTALLATION

### Requirements

#### This app uses the Django REST framework.

* REST framework requires the following: 

    - Python (3.6, 3.7, 3.8, 3.9, 3.10, 3.11)
    - Django (3.0, 3.1, 3.2, 4.0, 4.1, 4.2)

```bash
    pip install django
    pip install djangorestframework
```

### Installation

**1. Clone the repository:**

```bash
    git clone https://github.com/MatthewDSummers/Starry-Ocean-API.git
```

**2. Your project settings.py:**

Project settings.py

```python
    # Application definition
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'other_app',
        'rest_framework',    # required for Starry Ocean
        'starry_ocean_api',  # Starry Ocean app
    ]
```

**3. Include Starry Ocean API in your project urls.py:**

Project urls.py:

```python
    from django.urls import path, include

    urlpatterns = [
        path('other-path/', include('other_app.urls')),
        path('starry-ocean/', include('starry_ocean_api.urls')) # Starry Ocean path
    ]
```
* * *



* * *

## 3. DATA TYPE

**Starry Ocean API returns the following data type:**
   - JSON

* * * 



* * * 
## 4. ENDPOINTS

### Calling the Host Directly

Alternatively, if you don't want to use the Django app provided, you can call the host directly using the following format:

`https://matthewsummers.dev/starry-ocean/{identifier}`

Replace `{identifier}` with the appropriate series or character information (see `List of Endpoints` below).


List of Endpoints
  -   `starry-ocean/series/{series_number}`
  -   `starry-ocean/series/{series_number}/characters/{character_name}`
  -   `starry-ocean/characters/{character_name}`
  -   `starry-ocean/characters/all`


#### 1. `starry-ocean/series/{series_number}`

Retrieve all characters from the specified Star Ocean series.

Calls for either Star Ocean 1 game will be handled simply by one endpoint: /starry-ocean/series/1

Likewise for Star Ocean 2: /starry-ocean/series/2

**Parameters:**

*   `{series_number}` string, required
    -   Expected values: '1' or '2'

**Example usage: /starry-ocean/series/1**

```json
{
    "Roddick Farrence": {
        "Name": "Roddick Farrence",
        "Description": "Roddick Farrence (ラティクス・ファーレンス, Ratikusu Fārensu, lit. Ratix Farrence) is the main protagonist of the first Star Ocean, as well as its remake Star Ocean: First Departure. In the Japanese version, he is affectionately called Rati (ラティ) by his friends. A young Fellpool from Roak, Roddick guards his hometown alongside his childhood friends, Millie Chliette and Dorne Murtough, until a mysterious plague threatens their peaceful lives.",
        "Race": "Fellpool",
        "Place of origin": "Border town of Kratus, Kingdom of Muah, Planet Roak",
        "Birthday": "January 14th, 327 S.D.",
        "Age": [
            "19"
        ],
        "Weapon": "Sword",
        "Height": "174 cm",
        "Weight": "68 kg",
        "Affiliation": [
            "Kratus Defense Force"
        ],
        "Occupation": "Guard",
        "Image": {
            "Star Ocean: First Departure R": "",
            "Star Ocean 1": true
        },
        "Series": "1"
    },
    "Millie Chliette": {
        "Name": "Millie Chliette",
        "Description": "Millie Chliette (ミリー・キリート, Mirī Kirīto, lit. Milly Kiliet) is one of the main characters of the first Star Ocean, as well as its remake, Star Ocean: First Departure. A young Fellpool, she is the daughter of Martoth Chliette, the hometown's healer, and as such, she is proficient in healing symbology herself. She is childhood friends with Roddick Farrence and Dorne Murtough.",
        "Race": "Fellpool",
        "Place of origin": "Border town of Kratus, Kingdom of Muah, Planet Roak",
        "Birthday": "July 15th, 328 S.D.",
        "Age": [
            "18"
        ],
        "Weapon": "Rod",
        "Height": "164 cm",
        "Weight": "46 kg",
        "Affiliation": [
            "Kratus Defense Force"
        ],
        "Occupation": "Guard",
        "Image": {
            "Star Ocean: First Departure R": "",
            "Star Ocean 1": true
        },
        "Series": "1"
    }
}
```



#### 2. `starry-ocean/series/{series_number}/characters/{character_name}`

Direct look-up to retrieve a specific character from a specific series.

**Parameters:**

*   `{series_number}` string, required
    -   Expected values: '1' or '2'
*   `{character_name}` string, required
    -   Example value: 'Cyuss Warren'

**Example usage: /starry-ocean/series/1/characters/Cyuss Warren**

```json
{
    "Name": "Cyuss Warren",
    "Description": "Cyuss Warren (シウス・ウォーレン, Shiusu Wōren, lit. Cius Warren) is a main character in the first Star Ocean, as well as its remake Star Ocean: First Departure. A combative former Knight of Astral, he wanders the land training to become a swordsman of legend.",
    "Race": "Highlander",
    "Place of origin": "Astral Kingdom, Planet Roak",
    "Birthday": "November 8th, 26 S.D.",
    "Age": [
        "20 (SO1)",
        "23 (SO1FD)"
    ],
    "Weapon": "Doublehanded Sword",
    "Height": "190 cm",
    "Weight": "90 kg",
    "Affiliation": [
        "Astral Knights (formerly)"
    ],
    "Occupation": "Knight (formerly)",
    "Image": {
        "Star Ocean: First Departure R": "",
        "Star Ocean 1": true
    },
    "Series": "1"
}
```


#### 3. `starry-ocean/characters/{character_name}`

Retrieve a single character by providing a partial or exact character name.

**Parameters:**

*   `{character_name}` string, required
    - Example value: 'Rena'

**Example usage: /starry-ocean/characters/Rena**

```json
{
    "Name": "Rena Lanford",
    "Description": "Rena Lanford (レナ・ランフォード, Rena Ranfōdo, lit. Rena Lanford) is one of the two protagonists of Star Ocean: The Second Story, its enhanced port Second Evolution and remake The Second Story R, and its sequel Blue Sphere, alongside Claude C. Kenny. Blessed with healing abilities that no one else on Expel possesses, she longs to discover who she actually is, knowing that her parents are not her biological ones.",
    "Birthday": "May 13, S.D. 349",
    "Age": [
        "17"
    ],
    "Weapon": "Cestus",
    "Height": "161cm",
    "Weight": "45kg",
    "Affiliation": [],
    "Occupation": "Student",
    "Image": {
        "Star Ocean: The Second Story R": true,
        "Star Ocean: The Second Story": true
    },
    "Series": "2"
}
```

#### 4. `starry-ocean/characters/all`

Retrieve all characters from Star Ocean 1 and Star Ocean 2.

```json
{
    "STAR_OCEAN_ONE": {
        "CHARACTERS": {
            "Roddick Farrence": {
                "Name": "Roddick Farrence",
                "Description": "Roddick Farrence (ラティクス・ファーレンス, Ratikusu Fārensu, lit. Ratix Farrence) is the main protagonist of the first Star Ocean, as well as its remake Star Ocean: First Departure. In the Japanese version, he is affectionately called Rati (ラティ) by his friends. A young Fellpool from Roak, Roddick guards his hometown alongside his childhood friends, Millie Chliette and Dorne Murtough, until a mysterious plague threatens their peaceful lives.",
                "Race": "Fellpool",
                "Place of origin": "Border town of Kratus, Kingdom of Muah, Planet Roak",
                "Birthday": "January 14th, 327 S.D.",
                "Age": [
                    "19"
                ],
                "Weapon": "Sword",
                "Height": "174 cm",
                "Weight": "68 kg",
                "Affiliation": [
                    "Kratus Defense Force"
                ],
                "Occupation": "Guard",
                "Image": {
                    "Star Ocean: First Departure R": "",
                    "Star Ocean 1": true
                },
                "Series": "1"
            },
            "Millie Chliette": {
                "Name": "Millie Chliette",
                "Description": "Millie Chliette (ミリー・キリート, Mirī Kirīto, lit. Milly Kiliet) is one of the main characters of the first Star Ocean, as well as its remake, Star Ocean: First Departure. A young Fellpool, she is the daughter of Martoth Chliette, the hometown's healer, and as such, she is proficient in healing symbology herself. She is childhood friends with Roddick Farrence and Dorne Murtough.",
                "Race": "Fellpool",
                "Place of origin": "Border town of Kratus, Kingdom of Muah, Planet Roak",
                "Birthday": "July 15th, 328 S.D.",
                "Age": [
                    "18"
                ],
                "Weapon": "Rod",
                "Height": "164 cm",
                "Weight": "46 kg",
                "Affiliation": [
                    "Kratus Defense Force"
                ],
                "Occupation": "Guard",
                "Image": {
                    "Star Ocean: First Departure R": "",
                    "Star Ocean 1": true
                },
                "Series": "1"
            }
        }
    },
    "STAR_OCEAN_TWO": {
        "CHARACTERS": {
            "Claude C. Kenny": {
                "Name": "Claude C. Kenny",
                "Description": "Claude C. Kenny (クロード・Ｃ・ケニー, Kurōdo C. Kenī, lit. Crawd C. Kenny) is the son of the famous Admiral Ronyx J. Kenny, a main character from the original Star Ocean. Although Claude has the ability and talent to be an officer, he lives in the shadow of his father. Generally a nice guy, Claude is passionate about what he thinks is right. Claude is one of the two protagonists of Star Ocean: The Second Story, its enhanced port, Second Evolution, its remake, The Second Story R, and its sequel Blue Sphere, alongside Rena Lanford. His surname was originally translated as Kenni in The Second Story.",
                "Race": "Earthling",
                "Place of origin": "Planet Earth",
                "Birthday": "January 23, S.D. 347",
                "Age": [
                    "19"
                ],
                "Weapon": "Sword",
                "Height": "175cm",
                "Weight": "68kg",
                "Affiliation": [
                    "Pangalactic Federation",
                    "FSS-6004C Calnus crew"
                ],
                "Occupation": "Military officer",
                "Image": {
                    "Star Ocean: The Second Story R": true,
                    "Star Ocean: The Second Story": true
                },
                "Series": "2"
            },
            "Rena Lanford": {
                "Name": "Rena Lanford",
                "Description": "Rena Lanford (レナ・ランフォード, Rena Ranfōdo, lit. Rena Lanford) is one of the two protagonists of Star Ocean: The Second Story, its enhanced port Second Evolution and remake The Second Story R, and its sequel Blue Sphere, alongside Claude C. Kenny. Blessed with healing abilities that no one else on Expel possesses, she longs to discover who she actually is, knowing that her parents are not her biological ones.",
                "Birthday": "May 13, S.D. 349",
                "Age": [
                    "17"
                ],
                "Weapon": "Cestus",
                "Height": "161cm",
                "Weight": "45kg",
                "Affiliation": [],
                "Occupation": "Student",
                "Image": {
                    "Star Ocean: The Second Story R": true,
                    "Star Ocean: The Second Story": true
                },
                "Series": "2"
            }
        }
    }
}
```
* * * 



* * *
## 5. ERRORS

### All errors will return appropriate HTTP response codes accompanied by the following JSON error object.

**Example error call**

```javascript
function call_the_api(){
    $.ajax({
        url:"https:/project-url/starry-ocean/characters",
        method: "GET",
        dataType: "json",
        success: function(data){
            console.log("Success", data)
        },
        error: function (xhr, status, error) {

            // GENERIC ERROR RESPONSE 
            console.error("XHR Status:", xhr.status);
            console.error("Status:", status);
            console.error("Error:", error);

            // DETAILED ERROR RESPONSE
            var error_data = JSON.parse(xhr.responseText);
            console.log("Error data:", error_data);
        }
    });
}
call_the_api()
```
**Example error response**

XHR Status: 400

Status: error

Error: Bad Request

Error data:

```javascript
{
    "error_data": {
        "code": 400,
        "message": "Bad Request",
        "details": "Please provide a character name"
    }
}
```

* * *
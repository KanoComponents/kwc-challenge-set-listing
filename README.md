# \<kwc-challenge-set-listing\>

## Purpose
To display all the step-by-step challenge sets available to the user.

 ## Properties
 * challengeSets: An array of challenge set objects. A `<kwc-challenge-set>` element is rendered for each set.
 * userAvatarUrl: An url for the current user's avatar. This will be used as the current challenge icon in the progress bar if present.
 * completedChallenges: A dictionary of challenge categories containing an array of challenge ids that have been completed for each category.

The `challengeSets` and `completedChallenges` property has the shape (specified using [json schema](https://spacetelescope.github.io/understanding-json-schema/)):

```js
// challengeSets
{
    type: 'array',
    items: {
        type: 'object',
        properties: {
            title: {
                type: 'string'
            },
            description: {
                type: 'string'
            },
            category: {
                type: 'string'
            },
            medal-disabled:{
                type: 'string',
                format: 'url'
            },
            medal-enabled: {
                type: 'string',
                format: 'url'
            },
            challenges: {
                type: 'array',
                items:{
                    type: 'object',
                    properties: {
                        title: {
                            type: 'string'
                        },
                        slug: {
                            type: 'string'
                        }
                    },
                    required: [ 'title', 'slug' ]
                }
            }
        }
    }
}
// e.g
{
[
    {
        "title": "Flash and draw the lights",
        "description": "Turn on lights, change colors, make them move and sparkle. Paint pictures, learn to make frame by frame animations.",
        "category": "kano-code-challenges-pixel-intro",
        "medal-disabled": "static/challenges/training/pixel_medal_disabled.svg",
        "medal-enabled": "static/challenges/training/pixel_intro.svg",
        "challenges": [
            {
                "title": "Pixel lights on",
                "slug": "pixel_intro_1"
            },
            {
                "title": "Pixel color picker",
                "slug": "pixel_intro_2"
            },
            {
                "title": "Pixel color random loop",
                "slug": "pixel_intro_3"
            },
            {
                "title": "Pixel point",
                "slug": "pixel_intro_4"
            }
        ]
    },
    {
        "title": "Microphone magic",
        "description": "Use the Pixel Kit microphone, make lights dance to music, turn on and off when you clap. Scream, shout, sing.",
        "category": "kano-code-challenges-pixel-mic",
        "medal-disabled": "static/challenges/training/pixel_medal_disabled.svg",
        "medal-enabled": "static/challenges/training/pixel_mic.svg",
        "challenges": [
            {
                "title": "Microphone 1",
                "slug": "pixel_mic_1"
            },
            {
                "title": "Microphone 2",
                "slug": "pixel_mic_2"
            },
            {
                "title": "Microphone 3",
                "slug": "pixel_mic_3"
            },
            {
                "title": "Microphone 4",
                "slug": "pixel_mic_4"
            },
            {
                "title": "Microphone 5",
                "slug": "pixel_mic_5"
            }
        ]
    }
]

//completedChallenges (TODO: Sorry, not a json scheme yet.)
{
    type: 'object',
    properties: {
        "<challenge category>" : {
            type: 'number'
        }
    }
}
//e.g.
{
    "kano-code-challenges-pixel-intro": 1,
    "kano-code-challenges-pixel-mic": 5
}

```

## Events
This component will fire a custom event `open-kano-code` intitated by a click or tap event on any of the challenge circles or the continue button in any of the challenge set elements. The event is passed the following detail:
```js
{
    type: 'object',
    properties: {
        type: {
            type: 'string'
        },
        challengeId: {
            type: 'string'
        }
    }
}
```
The challengeId can then be accessed in any listener implementation on the event detail property.
```js
addEventListener('open-kano-code', function(e){
    console.log(e.detail);
}
// e.g. {"type": "challenge", "challengeId: "pixel_talking_mouth"}
```

## Installation
* Clone this repository.
* Run `bower i`
* Make sure you have the [Polymer CLI](https://www.npmjs.com/package/polymer-cli) installed. Then run `polymer serve` to serve your element locally.

## Running Tests

```
$ polymer test --skip-plugin junit-reporter
```

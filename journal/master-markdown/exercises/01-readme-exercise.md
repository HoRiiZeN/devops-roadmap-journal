# README Exercise
---

This is a sample README file for an exercise.

## Fun Fact About Cats

Did you know that cats are great pets? They are independent, playful, and can be very affectionate. I love them!

## Pizza Toppings Rating

| Pizza Toppings | Rating      |
| -------------- | ----------- |
| Pepperoni      | 10          |
| Mushrooms      | 8           |
| Onions         | 4           |
| Sausage        | 9           |
| Bacon       | 0<sup>[1]</sup>      |)* |

<sup>[1]</sup> *bacon haram*.

## Script that recommends the perfect phone brand

```bash
#!/bin/bash
echo "Hello there! I will help you to choose what phone brand is best for you by simply asking you 1 single question."

echo "Do you prefer iOS or Android? (Type 'iOS' or 'Android')"
read answer

if [ "$answer" != "Android" ]; then
  echo "Bad choice. You should go for an Android phone."
  echo "Try again. Type 'Android':"
  read answer
fi

if [ "$answer" = "Android" ]; then
  echo "Great choice! You can choose from popular Android brands like Samsung, Google, or OnePlus."
else
  echo "Still not Android, huh? Well, good luck out there."
fi
```

## My Favorite Music Genres (No Particular Order)

- Moroccan Rap
- Arabic Hip Hop
- Moroccan Pop
- Vocaloid
- J-Pop
- Anime
-  Hyperpop
- Pop
- Glitch
- J-Rock
- Speedcore
- K-Pop
- Raï
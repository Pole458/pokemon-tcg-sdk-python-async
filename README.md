# Pokémon TCG SDK

This is an async adaption of the [Pokémon TCG SDK for Python](https://github.com/PokemonTCG/pokemon-tcg-sdk-python). It is a wrapper around the Pokémon TCG API of [pokemontcg.io](http://pokemontcg.io/).

## Requirements
Python >= 3.6

This library uses [aiohttp](https://docs.aiohttp.org/en/stable/). The documentation suggests installing this two optional library:
 - [cchardet](https://pypi.python.org/pypi/cchardet/): cChardet is high speed universal character encoding detector - binding to charsetdetect.
 - [aiodns](https://pypi.python.org/pypi/aiodns): DNS resolver for asyncio.
 
## Usage

Wrap all the coroutines that needs to use the API inside one AsyncClientContext().
The AsyncClientContext will automatically open and close the underlying aiohttp session.
You can also wrap your entire application.

    async with AsyncClientContext(api_key='12345678-1234-1234-1234-123456789ABC'):
        await all_your_coroutines_that_use_the_api()

Import (Card and Set will be most used)

    from pokemontcgsdk import Card
    from pokemontcgsdk import Set
    from pokemontcgsdk import Type
    from pokemontcgsdk import Supertype
    from pokemontcgsdk import Subtype
    from pokemontcgsdk import Rarity

### Classes

    Card
    Set
    Type
    Supertype
    Subtype
    Rarity

### Properties Per Class

#### Card

    abilities
    artist
    ancientTrait
    attacks
    convertedRetreatCost
    evolvesFrom
    flavorText
    hp
    id
    images
    legalities
    regulationMark
    name
    nationalPokedexNumbers
    number
    rarity
    resistances
    retreatCost
    rules
    set
    subtypes
    supertype
    tcgplayer
    types
    weaknesses

#### Set

    id
    images
    legalities
    name
    printedTotal
    ptcgoCode
    releaseDate
    series
    total
    updatedAt

### Functions Available

#### Find a card by id

    card = await Card.find('xy1-1').get()

#### Filter Cards via query parameters

    # List (may take a while)
    cards = await Card.where(q='set.name:generations supertype:pokemon').get()
    
    # Generator
    async for card in Card.where(q='set.name:generations supertype:pokemon').generator():
        ...

#### Find all cards

    # List (will take a while)
    cards = await Card.all().get()

    # Generator
    async for card in Card.all().generator():
        ...

#### Get all cards, but only a specific page of data

    cards = await Card.where(page=5, pageSize=250).get()

#### Find a set by code

    set = await Set.find('base1').get()

#### Filter sets via query parameters

    # List
    sets = await Set.where(q='legalities.standard:legal').get()

    # Generator
    async for set in Set.where(q='legalities.standard:legal').generator():
        ...

#### Get all Sets
    
    # List
    sets = await Set.all().get()

    # Generator
    async for set in Set.all().generator():
        ...

#### Get all Types

    types = await Type.all().get()

#### Get all Subtypes

    subtypes = await Subtype.all().get()

#### Get all Supertypes

    supertypes = await Supertype.all().get()

#### Get all Rarities

    rarities = await Rarity.all().get()

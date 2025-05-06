#!/bin/zsh
trap 'rm -f /tmp/raw_species.json' EXIT
trap 'rm -f /tmp/raw_evolution.json' EXIT

API_URL="https://pokeapi.co/api/v2/"
VERSION="1.0.0"

# Flags
pokemon=""
types=false
forms=false
help=false

# Fancy Formating
BOLD="\e[1m"
RESET="\e[0m"
MAGENTA="\e[35m"
UNDERLINE="\e[4m"

# Container Variables
curled=""
stage_one=null
stage_two=null

# Set All Pokemon Variables
allpokemon() {
    forms=true
    types=true
}

# Flag Settings
while [[ "$#" -gt 0 ]]
do case $1 in
    -p|--pokemon) pokemon="$2"
    shift 2;;
    -t|--types) types=true
    shift;;
    -f|--forms) forms=true
    shift;;
    -a|--all-pokemon) allpokemon
    shift;;
    -h|--help) help=true
    shift;;
    -v|--version)
        echo "Pokefetcher v$VERSION"
        exit 0
    shift;;
    *) echo "Unknown option: $1"
    exit 1
    ;;
esac
done

# Species Data Fetch
speciesfetch() {
    species_url=$(echo "$curled" | jq -r '.species.url')
    species_data=$(curl -s "$species_url" > /tmp/raw_species.json)
}

# Types
typesfetch() {
    if $types; then
        echo "${BOLD}Types${RESET}:"
        echo "$curled" | jq -r '.types[].type.name' | sed 's/^/  /'
    fi
}

# Forms
formsfetch() {
    if $forms; then
        echo "${BOLD}Forms${RESET}:"
        cat /tmp/raw_species.json | jq -r '.varieties[].pokemon.name' | sed 's/^/  /'
    fi
}

# Evolutions
evosfetch() {
    evolution_url=$(cat /tmp/raw_species.json | jq -r '.evolution_chain.url')
    evolution_data=$(curl -s "$evolution_url" > /tmp/raw_evolution.json)
    evolutions=$(cat /tmp/raw_evolution.json | jq -r '.chain.evolves_to[]')

    stage_one=$(echo $evolutions | jq -r '.evolves_to[].species.name')
    stage_two=$(echo $evolutions | jq -r '.species.name')

    echo "${UNDERLINE}$pokemon${RESET} ${UNDERLINE}$stage_one${RESET} ${UNDERLINE}$stage_two${RESET}\n"
}

# Main Function
pokefetch() {
    # Curl the API
    pokemon=$1
    curled=$(curl -s $API_URL/pokemon/$pokemon)

    # Handle Invalid Pokemon
    if [[ -z "$curled" || "$curled" == "Not Found" ]]; then
        echo "Error: Pokémon '$pokemon' not found."
        exit 1
    fi

    # Echo Name and ID
    name=$(echo "$curled" | jq -r .name | awk '{print toupper(substr($0,1,1)) tolower(substr($0,2))}')
    id=$(echo "$curled" | jq -r .id)
    echo "${BOLD}${MAGENTA}$name${RESET}, ID:${BOLD}$id${RESET}"

    # Curl the pokemon-species page for evosfetch and formsfetch
    speciesfetch

    # Call Aux. Functions
    evosfetch
    typesfetch
    formsfetch
}

help() {
    echo "Welcome to Pokefetcher, a simple PokeAPI interface!\n\nUse:\n pokefetcher -p <pokemon> [flags]\n\nFlags:\n -t, --types       Displays the Pokemon's Typing\n -f, --forms       Displays Variant forms (Regional, GMAX, Mega...)\n -a, --all-pokemon Acts as both --types and --forms\n -h, --help        Displays this here help message!\n -v, --version     Displays current Pokefetcher version"
}

if $help; then
    help
elif [[ "$pokemon" != "" ]]; then
    pokefetch "$pokemon"
else
    echo "Usage: $0 -p <pokemon> [-t] [-f]"
fi
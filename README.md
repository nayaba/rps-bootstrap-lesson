# Adding Bootstrap to Rock, Paper, Scissors

- Visit bootstrap docs
- Add CDN link for both css and js
- Show how bootstrap immediately adds styling
- Show difference between putting bootsrap BELOW our CSS link versus ABOVE
- Add a `How to Play` button outside of the main tags (note which style sheet is being applied)
- Update our CSS `button` rule to be `main > button` so that our new button uses bootstrap styling
    - Wrap all of our content in a `<div>` with a class of `container`
    - Update our `html, body` rule to `.container`
- Show how bootstrap classes work by adding `btn btn-primary` classes to new button
- Talk about the different [colors (danger, warning, etc.)](https://getbootstrap.com/docs/5.3/components/buttons/#variants)
- Show the variety of Components bootstrap has to offer

### How to Play Modal

- Use the Modal from the docs to create a "How to Play" pop-up modal
- Edit the modal - remove the save button; give it a new title; add the following code snippet for instructions:
    - ```html
        <p><strong>1. Choose Your Move:</strong><br>
           Tap one of the buttons to select your move: 🪨 Rock, 📄 Paper, or ✂️ Scissors.</p>
        <p><strong>2. Wait for the Result:</strong><br>
           The computer will randomly pick a move.</p>
        <p><strong>3. Check Who Wins:</strong><br>
           - 🪨 Rock beats ✂️ Scissors<br>
           - ✂️ Scissors beats 📄 Paper<br>
           - 📄 Paper beats 🪨 Rock<br>
           - The same move is a tie!</p>
    ```
### Contact Us Page with Form

- Create a new html file in anticipation of adding a navbar.  It will be a contact form wrapped in our container div:
    - ```html
        <div class="container">
            <h1>Contact Us</h1>
                <form>
                    <label>Name:</label>
                    <input type="text">
                    <label>Message:</label>
                    <textarea></textarea>
                    <button>Submit</button>
                </form>
        </div>
    ```
- Navigate to `contact.html` to view the new form.  Notice that our bootstrap css is not applied here (nor is our custom css) - add the CDN link.
- Emphasize the need for both a better looking form and navigation.  Start with the form.
- Grab the example form from the [Form Control](https://getbootstrap.com/docs/5.3/forms/form-control/) section.  This snippet is only the name and text fields, so be sure not to delete your button or form tags.
- Style the submit button - visit the [Block buttons](https://getbootstrap.com/docs/5.3/components/buttons/#block-buttons) section of the docs to stretch the submit button out nicely.

### Adding a Navbar

- Grab the example navbar from [the docs](https://getbootstrap.com/docs/5.3/components/navbar/)
- Update the navbar logo with an image - grab a scissors icon from[Bootstrap Icons](https://icons.getbootstrap.com/#install).  First add the font import; then you can use the scissors icon.  Also mention SVGs (HTML snippet) that don't need the font and will be handled differently by CSS.
    - be sure to update this link to point back at `index.html`
- Remove all links except for Home - update it so that it navigates us back to `index.html`
- Remove the `active` class from Home 
- Add a Contact Us link
- Use the inspector to show how the navbar collapses into a hamburger... uh-oh it doesn't expand though!  Use this opportunity to show an example of why you also need the script tag (which we forgot on our contact us page).
- Go back to index.html and add our finished navbar.
- Show off how easy it is to [change navbar color](https://getbootstrap.com/docs/5.3/utilities/background/#background-color)
    - ```html
        <nav class="navbar navbar-expand-lg bg-primary navbar-dark">
        ```
    - Be sure to update the search button as well
    - ```html
        <button class="btn btn-outline-light" type="submit">Search</button>
        ```
- Have students update the `Contact Us` navbar to match

### Adding a Card
- Create a `stats.html` page
- Add boilerplate, plus CSS links and script links
- Create a `container` div for our main content
- Copy and paste navbar from previous pages
- Add Stats link to all three navbars - emphasize the repetitive nature of these tasks and mention how Single Page Applications in React are going to fix these problems.
- Grab a [Horizontal Card](https://getbootstrap.com/docs/5.3/components/card/#horizontal) from bootstrap docs
- Update the title to Player's Name
- Update the card body with stats:
    - ```html
        <div class="card-body">
            <h5 class="card-title">Player1</h5>
                <p>Games Played: 50</p>
                <p>Wins: 30 &nbsp; | &nbsp; Losses: 15 &nbsp; | &nbsp; Draws: 5</p>
                <p>Win Percentage: 60%</p>
                <p>Favorite Move: 🪨 Rock</p>
                <p class="card-text"><small class="text-body-secondary">Current Streak: 3 Wins</small></p>
        </div>
    ```
- Change the card `max-width` to `min-width` to look a bit nicer - `<div class="card mb-3" style="min-width: 540px;">`
- Grab a [person icon from bootstrap icons](https://icons.getbootstrap.com/icons/person/) - this time use an SVG and change the width and height to auto
- Copy and paste a few cards to show how this looks.  We'll need to update our css to make it look good.  Give the `container-div` on `stats.html` a new class of `container-stats`.  Create this new css rule:
    - ```css
        .container-stats {
            margin: 10px;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
        }
    ```
- Take this opportunity to talk about how nice it would be if you could re-use the same card, but populate it with different information (we'll tackle this in the level up)


### Level Up
Two concepts here - the first, addressing changing html in JS files via the innerHTML property and dynamically rendering content.

- Delete the cards in our `stats.html` page
- Let's add an arry of players to the top of our JS file (in the constants section):
```js
const players = [
  {
    name: "Player1",
    gamesPlayed: 50,
    wins: 30,
    losses: 15,
    draws: 5,
    winPercentage: "60%",
    favoriteMove: "🪨 Rock",
    streak: "3 Wins"
  },
  {
    name: "Player2",
    gamesPlayed: 40,
    wins: 25,
    losses: 10,
    draws: 5,
    winPercentage: "62.5%",
    favoriteMove: "📄 Paper",
    streak: "5 Wins"
  },
  {
    name: "Player3",
    gamesPlayed: 60,
    wins: 35,
    losses: 20,
    draws: 5,
    winPercentage: "58.3%",
    favoriteMove: "✂️ Scissors",
    streak: "2 Wins"
  }
]
```
- Cache our stats container `const statsContainerEl = document.querySelector('.container-stats')`
- Create a function called `renderStatsCards` whose purpose is to iterate through the array and dynamically display a card for each object
    - ```js
        const renderStatsCards = () => {
        players.forEach(player => {
            statsContainerEl.innerHTML += `
            <div class="card mb-3" style="min-width: 540px;">
                <div class="row g-0">
                <div class="col-md-4">
                    <svg xmlns="http://www.w3.org/2000/svg" width="auto" height="auto" fill="currentColor" class="bi bi-person" viewBox="0 0 16 16">
                        <path d="M8 8a3 3 0 1 0 0-6 3 3 0 0 0 0 6m2-3a2 2 0 1 1-4 0 2 2 0 0 1 4 0m4 8c0 1-1 1-1 1H3s-1 0-1-1 1-4 6-4 6 3 6 4m-1-.004c-.001-.246-.154-.986-.832-1.664C11.516 10.68 10.289 10 8 10s-3.516.68-4.168 1.332c-.678.678-.83 1.418-.832 1.664z"/>
                    </svg>
                </div>
                <div class="col-md-8">
                    <div class="card-body">
                    <h5 class="card-title">Player1</h5>
                    <p>Games Played: 50</p>
                    <p>Wins: 30 &nbsp; | &nbsp; Losses: 15 &nbsp; | &nbsp; Draws: 5</p>
                    <p>Win Percentage: 60%</p>
                    <p>Favorite Move: 🪨 Rock</p>
                    <p class="card-text"><small class="text-body-secondary">Current Streak: 3 Wins</small></p>
                    </div>
                </div>
                </div>
            </div>
            `
            })
        }
    ```
    - Update the HTML snippet to grab the info directly from each `player` object
- Final code
    - ```js
        const renderStatsCards = () => {
        players.forEach(player => {
            statsContainerEl.innerHTML += `
            <div class="card mb-3" style="min-width: 540px;">
                <div class="row g-0">
                <div class="col-md-4">
                    <svg xmlns="http://www.w3.org/2000/svg" width="auto" height="auto" fill="currentColor" class="bi bi-person" viewBox="0 0 16 16">
                        <path d="M8 8a3 3 0 1 0 0-6 3 3 0 0 0 0 6m2-3a2 2 0 1 1-4 0 2 2 0 0 1 4 0m4 8c0 1-1 1-1 1H3s-1 0-1-1 1-4 6-4 6 3 6 4m-1-.004c-.001-.246-.154-.986-.832-1.664C11.516 10.68 10.289 10 8 10s-3.516.68-4.168 1.332c-.678.678-.83 1.418-.832 1.664z"/>
                    </svg>
                </div>
                <div class="col-md-8">
                    <div class="card-body">
                    <h5 class="card-title">${player.name}</h5>
                    <p>Games Played: ${player.gamesPlayed}</p>
                    <p>Wins: ${player.wins} &nbsp; | &nbsp; Losses: ${player.losses} &nbsp; | &nbsp; Draws: ${player.draws}</p>
                    <p>Win Percentage: ${player.winPercentage}</p>
                    <p>Favorite Move: ${player.favoriteMove}</p>
                    <p class="card-text"><small class="text-body-secondary">Current Streak: ${player.streak}</small></p>
                    </div>
                </div>
                </div>
            </div>
            `
            })
        }

        renderStatsCards()
    ```

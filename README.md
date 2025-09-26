# 9Days-
Everyone has a need 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>9Days - Find House Help</title>
<style>
    * { box-sizing: border-box; margin: 0; padding: 0; font-family: Arial, sans-serif; }
    body { background-color: #f7f7f7; }
    header { background: #ff6f61; color: white; padding: 1rem; text-align: center; }
    nav { display: flex; justify-content: center; gap: 1rem; margin-top: 0.5rem; }
    nav a { color: white; text-decoration: none; font-weight: bold; }
    .container { max-width: 1200px; margin: 2rem auto; padding: 0 1rem; }
    .buttons { display: flex; justify-content: center; gap: 1rem; margin: 2rem 0; }
    .buttons button { padding: 1rem 2rem; border: none; background: #ff6f61; color: white; font-size: 1rem; cursor: pointer; border-radius: 5px; }
    .listings { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 1.5rem; }
    .card { background: white; padding: 1rem; border-radius: 10px; box-shadow: 0 3px 8px rgba(0,0,0,0.1); text-align: center; }
    .card img { width: 100px; height: 100px; border-radius: 50%; object-fit: cover; margin-bottom: 1rem; }
    footer { background: #333; color: white; text-align: center; padding: 1rem; margin-top: 2rem; }
    form { display: flex; flex-direction: column; gap: 1rem; max-width: 400px; margin: 2rem auto; }
    form input, form select, form button { padding: 0.75rem; border-radius: 5px; border: 1px solid #ccc; }
    form button { background: #ff6f61; color: white; border: none; cursor: pointer; font-weight: bold; }
    .filter { display: flex; justify-content: center; gap: 1rem; margin-bottom: 1.5rem; flex-wrap: wrap; }
    .rating { color: #ffbf00; font-weight: bold; }
</style>
</head>
<body>

<header>
    <h1>9Days</h1>
    <nav>
        <a href="#home">Home</a>
        <a href="#register">Register</a>
        <a href="#listings">Listings</a>
    </nav>
</header>

<section class="container" id="home">
    <h2 style="text-align:center; margin-bottom:1rem;">Find Trusted House Help in Your City</h2>
    <div class="buttons">
        <button onclick="scrollToRegister()">I Need Help</button>
        <button onclick="scrollToRegister()">I Offer Help</button>
    </div>
</section>

<section class="container" id="register">
    <h2 style="text-align:center; margin-bottom:1rem;">Register</h2>
    <form id="registerForm">
        <input type="text" placeholder="Name" required>
        <input type="text" placeholder="City" required>
        <select id="serviceType" required>
            <option value="">Select Service Type</option>
            <option value="Cook">Cook</option>
            <option value="Cleaner">Cleaner</option>
            <option value="Driver">Driver</option>
            <option value="Other">Other</option>
        </select>
        <input type="text" placeholder="Contact Info" required>
        <button type="submit">Register</button>
    </form>
</section>

<section class="container" id="listings">
    <h2 style="text-align:center; margin-bottom:1rem;">Available House Help</h2>
    <div class="filter">
        <input type="text" id="filterCity" placeholder="Filter by city">
        <select id="filterService">
            <option value="">Filter by service</option>
            <option value="Cook">Cook</option>
            <option value="Cleaner">Cleaner</option>
            <option value="Driver">Driver</option>
            <option value="Other">Other</option>
        </select>
        <button onclick="applyFilters()">Apply Filters</button>
        <button onclick="resetFilters()">Reset</button>
    </div>
    <div class="listings" id="profiles">
        <!-- Profiles will appear here -->
    </div>
</section>

<footer>
    &copy; 2025 9Days. All rights reserved.
</footer>

<script>
    let profiles = [
        {name: "Ramesh Kumar", city: "Delhi", service: "Cook", contact: "9876543210", img: "https://randomuser.me/api/portraits/men/32.jpg", rating: 4},
        {name: "Sita Sharma", city: "Delhi", service: "Cleaner", contact: "9123456780", img: "https://randomuser.me/api/portraits/women/44.jpg", rating: 5},
        {name: "Amit Verma", city: "Delhi", service: "Driver", contact: "9988776655", img: "https://randomuser.me/api/portraits/men/65.jpg", rating: 3},
        {name: "Sunita Rao", city: "Delhi", service: "Cook", contact: "9012345678", img: "https://randomuser.me/api/portraits/women/22.jpg", rating: 5}
    ];

    const profilesContainer = document.getElementById("profiles");

    function renderProfiles(list) {
        profilesContainer.innerHTML = "";
        list.forEach(profile => {
            const card = document.createElement("div");
            card.className = "card";
            card.innerHTML = `
                <img src="${profile.img}" alt="${profile.name}">
                <h3>${profile.name}</h3>
                <p>City: ${profile.city}</p>
                <p>Service: ${profile.service}</p>
                <p>Contact: ${profile.contact}</p>
                <p class="rating">Rating: ${"★".repeat(profile.rating)}${"☆".repeat(5-profile.rating)}</p>
            `;
            profilesContainer.appendChild(card);
        });
    }

    renderProfiles(profiles);

    document.getElementById("registerForm").addEventListener("submit", function(e){
        e.preventDefault();
        const name = this[0].value;
        const city = this[1].value;
        const service = this[2].value;
        const contact = this[3].value;
        const rating = Math.floor(Math.random()*5)+1; // random rating for demo
        const img = "https://randomuser.me/api/portraits/lego/" + Math.floor(Math.random()*10) + ".jpg"; // dummy image

        const newProfile = {name, city, service, contact, img, rating};
        profiles.push(newProfile);
        renderProfiles(profiles);
        alert("Registration successful! Your profile has been added.");
        this.reset();
        scrollToListings();
    });

    function scrollToRegister() {
        document.getElementById("register").scrollIntoView({behavior: "smooth"});
    }

    function scrollToListings() {
        document.getElementById("listings").scrollIntoView({behavior: "smooth"});
    }

    function applyFilters() {
        const city = document.getElementById("filterCity").value.toLowerCase();
        const service = document.getElementById("filterService").value;
        const filtered = profiles.filter(p => 
            (p.city.toLowerCase().includes(city)) && 
            (service === "" || p.service === service)
        );
        renderProfiles(filtered);
    }

    function resetFilters() {
        document.getElementById("filterCity").value = "";
        document.getElementById("filterService").value = "";
        renderProfiles(profiles);
    }
</script>

</body>
</html>

<script>
import Sidebar from "../lib/sidebar.svelte";
// imports from firebase
import {
    initializeApp
} from "firebase/app";
import {
    getFirestore,
} from "firebase/firestore";
import {
    firebaseConfig
} from '../../Firebase.js';
import {
    getAuth,
    createUserWithEmailAndPassword,
} from "firebase/auth";

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore();

export {
    auth,
    db
};

let sidebar_show = true;

let name = "";
let email = "";
let password = "";
let hasBeenClicked = false;

// submit form
/**
	 * @param {boolean} [hasBeenClicked]
	 */

// function to test if the form is valid
// testing all the fields
function handleSubmission(hasBeenClicked) {
    // validate
    if (hasBeenClicked && isValidName && isValidEmail && isValidPassword && isValidNoChars) {
        // trim
        let trimName = name.trim();
        let trimEmail = email.trim();
        let trimPassword = password.trim();

        // Initialize Firebase
        const auth = getAuth();
        const db = getFirestore();
        // Create user
        createUserWithEmailAndPassword(auth, trimEmail, trimPassword)
            .then((userCredential) => {
                // Subribed user
                const user = userCredential.user;
                alert('Subscribed!');
                // ... Route redirection
            })
            .catch((error) => {
                const errorCode = error.code;
                const errorMessage = error.message;
                // console.table(errorCode, errorMessage);
                // See error codes
            });
    } 
    
    if (hasBeenClicked && !isValidName || !isValidEmail || !isValidPassword || !isValidNoChars) {
        hasBeenClicked = false;
        sidebar_show = true;
    }
}

function validateEmail(email) {
    var emailRegEx = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return emailRegEx.test(String(email).toLowerCase());
}

function validateNochars(name) {
    var regex = /^[a-zA-Z]/i;
    return regex.test(name);
}

$: isValidName = name.length > 0;
$: isValidEmail = validateEmail(email);
$: isValidPassword = password.length >= 8;
$: isValidNoChars = validateNochars(name);

</script>

<style>
:root {
    --textColor1: #008cff;
    --textColor2: #fff;
    --textColor3: #737594;
}

* {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    margin: 0;
    padding: 0;
}

@font-face {
    font-family: "Oswald";
    src: url("../assets/fonts/oswald-light.ttf") format("truetype");
}

main {
    width: 100%;
    height: 100vh;
    background-image: url(../assets/img/nandhu-kumar.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    display: flex;
    justify-content: center;
    align-items: center;
    align-content: center;
    font-family: "Oswald";
}

label {
    display: block;
    margin-bottom: 10px;
}

.wrappers {
    position: relative;
    width: 80%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    height: 70vh;
    box-shadow:
        2.1px 2.1px 1.5px -52px rgba(0, 0, 0, 0.044),
        4.7px 4.6px 3.4px -52px rgba(0, 0, 0, 0.065),
        7.9px 7.7px 5.7px -52px rgba(0, 0, 0, 0.08),
        12px 11.6px 8.6px -52px rgba(0, 0, 0, 0.093),
        17.3px 16.8px 12.4px -52px rgba(0, 0, 0, 0.105),
        24.5px 23.7px 17.5px -52px rgba(0, 0, 0, 0.117),
        34.7px 33.7px 24.9px -52px rgba(0, 0, 0, 0.13),
        50.4px 48.9px 36.1px -52px rgba(0, 0, 0, 0.145),
        77.6px 75.4px 55.7px -52px rgba(0, 0, 0, 0.166),
        138px 134px 99px -52px rgba(0, 0, 0, 0.21);
    border-bottom-right-radius: 5rem;

}

section {
    display: flex;
    flex-direction: column;
    align-items: center;
    border-top-left-radius: 5rem;
    border-bottom-left-radius: 5rem;
    background-image: linear-gradient(to bottom, #363535, #2b2a2a, #202020, #161616, #080808);
    width: 30%;
    background: rgba(255, 255, 255, 0.25);
    backdrop-filter: blur(4px);
    -webkit-backdrop-filter: blur(4px);
    border: 1px solid rgba(255, 255, 255, 0.18);
    border-right: none;
}

.hall {
    width: 70%;
    background-image: url(../assets/img/nandhu-kumar.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    height: 70vh;
    border-top-right-radius: 5rem;
    border-bottom-right-radius: 5rem;

}

input {
    display: block;
    padding: 10px 15px;
    border: none;
}

.input-d-wrappers {
    display: flex;
    align-items: center;
}

.input-wrapper {
    margin-top: 1rem;
}

h1 {
    font-family: "Oswald";
    padding-top: 1rem;
    color: white;
    letter-spacing: 5px;
    font-size: 2.2rem;
    text-align: center;
    text-shadow: 2px 3px 5px rgba(53, 52, 52, 0.65);
}

p {
    font-family: "Oswald";
}

.lambda-text {
    margin-top: 1rem;
    text-align: center;
    font-family: "Oswald";
    font-size: 1.2rem;
    color: white;
    text-shadow: 2px 3px 5px rgba(53, 52, 52, 0.65);
}

.connectez {
    font-family: "Oswald";
    font-size: 1.2rem;
    color: #0000EE;
    text-shadow: 2px 3px 5px rgba(53, 52, 52, 0.65);
    cursor: pointer;
}

label {
    color: white;
    padding: .5rem;
    text-shadow: 2px 3px 5px rgba(53, 52, 52, 0.65);
}

.button {
    display: block;
    margin: 0 auto;
    margin-top: 2.5rem;
    min-height: 50px;
    padding: 13px 24px;
    font-family: "Oswald";
    font-size: 16px;
    line-height: 20px;
    font-weight: bold;
    text-transform: uppercase;
    text-align: center;
    border: none;
    border-radius: 4px;
    outline: none;
    box-shadow: none;
    background-color: transparent;
    background-position: top center;
    cursor: pointer;
    transition: 0.3s ease-in-out;
    transition-property: background, color;
    text-shadow: 2px 3px 5px rgba(53, 52, 52, 0.65);
}

.button1 {
    position: relative;
    display: block;
    color: white;
    border-radius: 26px;
    box-sizing: border-box;
    border: 2px solid transparent;
    background-color: #F4B518;
    background-clip: padding-box;
    overflow: hidden;
    z-index: 1;
    box-shadow: 5px 5px 10px #00000046;
}

.button1::before {
    content: '';
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    right: 0;
    border: 2px solid transparent;
    background-clip: padding-box, border-box;
    background-repeat: repeat-x;
    background-size: calc(100% + 2px * 2) calc(100% + 2px * 2);
    background-position: center;
    border-radius: 26px;
    z-index: -1;
    transition: border-color 0.2s;
}

.button1::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 70vmax;
    height: 70vmax;
    border-radius: 50%;
    background-image: linear-gradient(90deg, #008cff, #363535);
    transform-origin: center;
    transform: translate(-50%, -50%) scale(0);
    transition: transform 0.4s ease-in-out;
    z-index: -1;
}

.button1:hover {
    color: var(--textColor2);
}

.button1:hover::after {
    transform: translate(-50%, -50%) scale(1);
}

.button1:active {
    color: #c3c4d5;
}

.button1:focus {
    color: white;
}

.button1:focus::before {
    border-color: #00b8d9;
}

/*mobile */
@media (min-width: 375px) and (max-width: 414px) {
    section {
        width: 100%;
    }

    h1 {
        font-size: 1.4rem;
    }

    .hall {
        display: none;
    }

    input {
        padding: 5px 4px;
    }
}

/* For Laptop Resolution */
@media only screen and (min-width: 1000px) and (max-width: 1550px) {

    h1 {
        font-size: 1.5rem;
    }

    label {
        padding: .2rem;
    }

    .button {
        margin-top: 1.12rem;
    }
}
</style>

<main>

    <div class="wrappers">

        <section>
            <h1>Bienvenue <br />
                sur <br />
                ViaTools
            </h1>
            <div class="input-d-wrappers">
                <div class="input-wrapper">
                    <!-- Name test -->
                    <!-- svelte-ignore a11y-label-has-associated-control -->
                    <label>Full Name</label>
                    <input type="text" bind:value={name}/>
                    <!-- Email test -->
                    <!-- svelte-ignore a11y-label-has-associated-control -->
                    <label>Email</label>
                    <input type="text" bind:value={email} />
                    <!-- Password test -->
                    <!-- svelte-ignore a11y-label-has-associated-control -->
                    <label>Password</label>
                    <input type="password" bind:value={password} />
                    {#if password && password.length >=8}
                    ✔️
                    {/if}
                    {#if hasBeenClicked && !isValidName && !isValidEmail && !isValidPassword}
                    <Sidebar bind:show={sidebar_show}/>
                    {/if}
              

                    <p class="lambda-text">Vous avez déjà un compte ? <br />
                        <span class="connectez">Connectez vous</span>
                    </p>
                    <button class="button button1" on:click={(event) => {
                        hasBeenClicked = true;
                        handleSubmission(hasBeenClicked);
                        event.stopPropagation();
                    }}>

                        <span class="button-content">S'inscrire</span>
                    </button>
                </div>
            </div>
        </section>
            <div class="hall">
            </div>
    </div>
</main>

<script>
    import { Doc, FirebaseApp, docStore } from 'sveltefire';
    import { initializeApp } from 'firebase/app';
    import { updateDoc, setDoc, getFirestore, DocumentReference } from 'firebase/firestore';
    import { getAuth } from 'firebase/auth';
	import { getStorage } from 'firebase/storage';
    import { goto } from '$app/navigation';
    import 'charts.css';

    // Initialize Firebase
    const firebaseConfig = {
        apiKey: "AIzaSyDGpRbJyuhM1t3F5zxUM3neDgG69tZyIP8",
        authDomain: "office-vote.firebaseapp.com",
        databaseURL: "https://office-vote-default-rtdb.firebaseio.com",
        projectId: "office-vote",
        storageBucket: "office-vote.appspot.com",
        messagingSenderId: "946893048079",
        appId: "1:946893048079:web:1b31b6df09a5bd30bad67a"
    };

    const app = initializeApp(firebaseConfig);
    const firestore = getFirestore(app);
    const auth = getAuth(app);
    const storage = getStorage(app);

    const refer = "questions/dogcat";
</script>

<FirebaseApp {firestore} {auth} {storage}>
    <Doc ref="{refer}" let:data let:ref let:firestore>
        <div id="page">
            <div id="title">
                <h1>{data.title}</h1>
            </div>
            {#if ref != null}
            <div id="bttn-wrap">
                <button on:click={() => 
                {
                    updateDoc(ref, {option1: {name: data.option1.name, value: data.option1.value+=1}});
                     goto('thanks');
                }} id="op1">
                    <p>{data.option1.name}</p>
                </button>
                <button on:click={() => 
                    {
                        updateDoc(ref, {option2: {name: data.option2.name, value: data.option2.value+=1}});
                         goto('thanks');
                    }} id="op2">
                    <p>{data.option2.name}</p>
                </button>
            </div>
            {/if}
        </div>
    </Doc>

</FirebaseApp>

<style>
    #page {
        margin: -8px;
        padding: 0;
        color: #fafafa;
        font-family: Arial, Helvetica, sans-serif;
        height: 100vh;
        width: 100vw;
        background-color: salmon;
        display: flex;
        justify-content: space-evenly;
        flex-wrap: wrap;
    }

    #title {
        height: 20vh;
        width: 100%;
        text-align: center;
    }

    #title h1 {
        padding-top: 1vh;
        font-size: 4rem;
    }

    #page button {
        height: 78vh;
        width: 48vw;
        border: none;
        border-radius: 10px;
        
    }

    #op1 {
        background-color: mediumseagreen;
    }

    #op2 {
        background-color: navy;
    }

    #page button p {
        color:#fafafa;
        font-size: 2rem;
        font-weight: bolder;
        text-shadow: 1px 1px 1px #aaa;
        padding: 5px;
    }
</style>
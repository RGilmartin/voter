<script>
    import { Doc, FirebaseApp, docStore } from 'sveltefire';
    import { initializeApp } from 'firebase/app';
    import { getFirestore } from 'firebase/firestore';
    import { getAuth } from 'firebase/auth';
	import { getStorage } from 'firebase/storage';
    import 'charts.css';
    import  QRCode  from 'qrcode';

    import {page} from '$app/stores';
	import { onMount } from 'svelte';
	import Navbar from '../../../components/navbar.svelte';
    import QrNavigation from '../../../components/QrNavigation.svelte';
	import ResultsChart from '../../../components/resultsChart.svelte';
    const docID = $page.params.docID;

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


    const colors = ['#FFBA49', "#20A39E", "#ef5b5b", '#23001E'];

    //'https://comfy-khapse-87c828.netlify.app/vote/'+ docID

    onMount(() => {
        QRCode.toCanvas(document.getElementById('qr-code'), 'https://comfy-khapse-87c828.netlify.app/vote/'+ docID, {version: 6,});
    });

    
    
</script>

<FirebaseApp {auth} {firestore} {storage}>
    <slot />

    <div class="page">
        <Navbar/>
        <Doc ref="questions/{docID}" let:data>
            <ResultsChart data={data} />
        </Doc>
        <QrNavigation />
        
    </div>
</FirebaseApp>

<style>
    .page {
        margin: -8px;
        padding: 0;
        color: #FBFBFB;
        font-family: Arial, Helvetica, sans-serif;
        display: flex;
        justify-content: flex-start;
        align-items: center;
        flex-direction: column;
        height: 100vh;
        width: 100vw;
        background-color: #922D50;
    }
</style>
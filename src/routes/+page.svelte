<script>
    import { Doc, FirebaseApp, docStore } from 'sveltefire';
    import { initializeApp } from 'firebase/app';
    import { getFirestore } from 'firebase/firestore';
    import { getAuth } from 'firebase/auth';
	import { getStorage } from 'firebase/storage';
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


    const colors = ['#FFBA49', "#20A39E", "#ef5b5b", '#23001E'];
</script>

<FirebaseApp {auth} {firestore} {storage}>
    <slot />

    <div class="page">
        <Doc ref="questions/dogcat" let:data>
            <h2>{data.title}</h2>
            <div class="chart">
                <table id="dataChart" class="charts-css column multiple show-heading show-labels datasets-spacing-7">
                    <thead>
                        <tr>
                            <th scope="col"><p>{data.option1.name}</p></th>
                            <th scope="col"><p>{data.option2.name}</p></th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <th>{data.option1.name}</th>
                            <td style="--size: {data.option1.value/(parseInt(data.option1.value) + parseInt(data.option2.value))}"><p>{data.option1.value}</p></td>
                        </tr>
                        <tr>
                            <th>{data.option2.name}</th>
                            <td style="--size: {data.option2.value/(parseInt(data.option1.value) + parseInt(data.option2.value))}"><p>{data.option2.value}</p></td>
                        </tr>
                    </tbody>
                </table> 
            </div>
        </Doc>

        <div id="qr-show">
            <div id="qr-text">
                <h3>Want to Vote?</h3>
                <h5>Scan this qr code and it will take you where you want to go.</h5>
            </div>
            <div id="qr-code">
                <img src="./scan_qr.svg" alt="qr code to access voting">
            </div>
        </div>
    </div>
</FirebaseApp>

<style>

    .page {
        background-color: #FFBA49;
        animation: mymove 45s infinite
    }

@keyframes mymove {
  0% {background-color: #FFBA49;}
  25% {background-color: #ef5b5b;}
  50% {background-color: #20A39E;}
  75% {background-color: #23001E;}
  100% {background-color: #FFBA49;}
}

    .page {
        margin: -8px;
        padding: 0;
        color: #fafafa;
        font-family: Arial, Helvetica, sans-serif;
        display: flex;
        justify-content: space-evenly;
        align-items: start;
        flex-direction: column;
        height: 100vh;
        width: 100vw;
    }

    #dataChart td{
        background-color: white;
        border-radius: 5px;
    }

    #dataChart td p {
        margin-top: -3rem;
        font-size: 2.8rem;
        font-weight: bold;
    }

    #dataChart tbody th {
        font-size: 1.5rem;
        margin-top: 84%;
        font-weight: bold;
    }

    h2 {
        font-size: 5rem;
        padding-left: 4rem;
    }

    .chart {
        width: 35%;
        align-self: center;
    }

    #qr-show {
        height: 15rem;
        width: 30rem;
        background-color: #464F51;
        align-self: center;
        margin-top: 7rem;
        border-radius: 10px;
        border: 3px solid rgb(17, 29, 29);
        display: flex;
        text-align: center;
    }
    #qr-text {
        width: 50%;
        text-align: left;
        padding: 20px 10px 0px 10px;
    }

    #qr-text h3 {
        font-weight: bold;
        font-size: 1.9rem;
    }

    #qr-text h5 {
        font-weight: 400;
        font-size: .9rem;
    }

    #qr-code {
        width: 50%;
    }
    
    #qr-code img {
        height: 90%;
        padding-top: 5%;
    }
</style>
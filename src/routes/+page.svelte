<script>
    import { Doc, FirebaseApp, docStore } from 'sveltefire';
    import { initializeApp } from 'firebase/app';
    import { getFirestore } from 'firebase/firestore';
    import { getAuth } from 'firebase/auth';
	import { getStorage } from 'firebase/storage';
    import 'charts.css';
	import internal from 'stream';

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
</script>

<FirebaseApp {auth} {firestore} {storage}>
    <slot />
    <h1>hello</h1>
    <Doc ref="questions/dogcat" let:data>
        <h2>{data.title}</h2>
        <div class="chart">
            <p>{data.Dog}</p>
            <p>{data.option1.name}: {data.option1.value}</p>
            <table class="charts-css column multiple show-heading show-labels show-primary-axis show-data-axes show-2-secondary-axes show-5-secondary-axes">
                <thead>
                    <tr>
                        <th scope="col">{data.option1.name}</th>
                        <th scope="col">{data.option2.name}</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <th>{data.option1.name}</th>
                        <td style="--size: calc( {data.option1.value / (data.option1.value + data.option2.value)} )">{(parseInt(data.option1.value) / (parseInt(data.option1.value) + parseInt(data.option2.value))).toString()}</td>
                    </tr>
                    <tr>
                        <th>{data.option2.name}</th>
                        <td style="--size: .5">4</td>
                    </tr>
                </tbody>
            </table> 
        </div>
    </Doc>
</FirebaseApp>
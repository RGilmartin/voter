<div id='title'>
    <div>
        <span>Simple</span>
        <span>V</span>
        <span>ote</span>
    </div>
    <div>
        <ul>
            <li><a href="/login">login or signup</a></li>
        </ul>
    </div>
</div>

<style>
    #title {
        width: 90%;
        display: flex;
        justify-content: space-between;
        align-items: baseline;
    }

    #title li {
        list-style: none;
    }

    #title a {
        color: #151515;
        text-decoration: none;
        font-size: 1rem;
        padding: .7rem 1.5rem;
        background-color: #fbfbfb;
        border-radius: 5px;
    }

    #title span:nth-child(odd) {
        font-size: 2rem;
        font-weight: 200;
    }

    #title span:nth-child(even) {
        font-size: 2.9rem;
        font-weight: bolder;
        margin: 0px -10px 0px -10px;
    }
</style>
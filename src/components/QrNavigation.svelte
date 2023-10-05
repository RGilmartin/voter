<div id="qr-show">
    <div id="qr-text">
        <h3>Want to Vote?</h3>
        <h5>Scan this qr code and it will take you where you want to go.</h5>
    </div>
    <canvas id="qr-code">
    </canvas>
</div>

<style>
     #qr-show {
        height: 15rem;
        width: 30rem;
        background-color: #151515;
        align-self: center;
        margin-top: 7rem;
        border-radius: 10px;
        box-shadow: 2px 3px 5px #151515;
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
        margin: auto;
        border-radius: 10px;
        border: 2px solid rgb(17, 29, 29);
    }
</style>
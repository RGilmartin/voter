<script lang="ts">
	import type { DocumentData } from "firebase/firestore";
    export let data: DocumentData;
</script>

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
                    <td style="--size: {parseInt(data.option1.value)/(parseInt(data.option1.value) + parseInt(data.option2.value))}"><p>{data.option1.value}</p></td>
            </tr>
            <tr>
                <th>{data.option2.name}</th>
                <td style="--size: {parseInt(data.option2.value)/(parseInt(data.option1.value) + parseInt(data.option2.value))}"><p>{data.option2.value}</p></td>
                </tr>
        </tbody>
    </table> 
</div>

<style>
    .chart {
        width: 35%;
        align-self: center;
    }

    #dataChart td{
        background-color: #FBFBFB;
        box-shadow: 2px 2px 3px #383838;
        border-radius: 5px;
    }

    #dataChart td p {
        margin-top: -3rem;
        font-size: 2.8rem;
        font-weight: bold;
        text-shadow: 2px 2px 3px #383838;
    }

    #dataChart tbody th {
        font-size: 1.5rem;
        margin-top: 84%;
        font-weight: bold;
    }

    h2 {
        font-size: 5rem;
        padding-left: 4rem;
        align-self: flex-start;
    }
</style>
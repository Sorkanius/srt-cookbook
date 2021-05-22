# Latency Negotiation Bootstrap

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x" crossorigin="anonymous">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.min.js" integrity="sha384-Atwg2Pkwv9vp0ygtn1JAojH0nYbwNJLPhwyoVbhoPwBhjQPR5VtM2+xf0Uwh9KtT" crossorigin="anonymous"></script>


<!-- Readonly input -->

## Configured Latency (Before Connection)

<div class="container">
    <div class="row">
        <div class="col-sm-2">
            <b>Peer A:</b>
        </div>
        <div class="col-md">
            <div class="form-floating">
                <input type="number" id="RcvLatencyA" class="form-control">
                <label for="RcvLatencyA">SRTO_RCVLATENCY</label>
            </div>
        </div>
        <div class="col-md">
            <div class="form-floating">
                <input type="number" id="PeerLatencyA" class="form-control">
                <label for="PeerLatencyA">SRTO_PEERLATENCY</label>
            </div>
        </div>
    </div>
    <div class="row">
        <div class="col-sm-2">
            <b>Peer B:</b>
        </div>
        <div class="col">
            <div class="form-floating">
                <input type="number" id="RcvLatencyB" class="form-control">
                <label for="RcvLatencyB">SRTO_RCVLATENCY</label>
            </div>
        </div>
        <div class="col">
            <div class="form-floating">
                <input type="number" id="PeerLatencyB" class="form-control">
                <label for="PeerLatencyB">SRTO_PEERLATENCY</label>
            </div>
        </div>
    </div>
</div>

<button class="btn btn-primary mb-3" id="ResetDefaultBtn">Reset to Defaults</button>


## Negotiated Latency (After Connection)


<div class="container">
    <div class="row">
        <div class="col-sm-2">
            <b>Peer A:</b>
        </div>
        <div class="col">
            <div class="form-floating sm-2">
                <input type="number" id="FinalRcvLatencyA" class="form-control sm-2" readonly>
                <label for="FinalRcvLatencyA">SRTO_RCVLATENCY</label>
            </div>
        </div>
        <div class="col-md">
            <div class="form-floating mb-3">
                <input type="number" id="FinalPeerLatencyA" class="form-control" readonly>
                <label for="FinalPeerLatencyA">SRTO_PEERLATENCY</label>
            </div>
        </div>
    </div>
    <div class="row">
        <div class="col-sm-2">
            <b>Peer B:</b>
        </div>
        <div class="col">
            <input type="number" id="FinalRcvLatencyB" class="form-control" readonly>
        </div>
        <div class="col">
            <input type="number" id="FinalPeerLatencyB" class="form-control" readonly>
        </div>
    </div>
</div>

<script>
    var RcvLatencyA = document.getElementById("RcvLatencyA");
    var PeerLatencyA = document.getElementById("PeerLatencyA");
    var RcvLatencyB = document.getElementById("RcvLatencyB");
    var PeerLatencyB = document.getElementById("PeerLatencyB");
    var FinalRcvLatencyA = document.getElementById("FinalRcvLatencyA");
    var FinalPeerLatencyA = document.getElementById("FinalPeerLatencyA");
    var FinalRcvLatencyB = document.getElementById("FinalRcvLatencyB");
    var FinalPeerLatencyB = document.getElementById("FinalPeerLatencyB");
    var ResetDefaultBtn = document.getElementById("ResetDefaultBtn");

    updateRcvAPeerB = function () {
        let val = Math.max(RcvLatencyA.value, PeerLatencyB.value);
        FinalRcvLatencyA.value = val;
        FinalPeerLatencyB.value = val;
    };

    updateRcvBPeerA = function () {
        let val = Math.max(RcvLatencyB.value, PeerLatencyA.value);
        FinalRcvLatencyB.value = val;
        FinalPeerLatencyA.value = val;
    };

    resetDefault = function() {
        RcvLatencyA.value = 120;
        RcvLatencyB.value = 120;
        PeerLatencyA.value = 0;
        PeerLatencyB.value = 0;
        updateRcvAPeerB();
        updateRcvBPeerA();
    }

    document.addEventListener('DOMContentLoaded', function() {
        resetDefault();
    }, true);
    ResetDefaultBtn.addEventListener("click", resetDefault);

    RcvLatencyA.addEventListener("input", updateRcvAPeerB);
    PeerLatencyB.addEventListener("input", updateRcvAPeerB);
    RcvLatencyB.addEventListener("input", updateRcvBPeerA);
    PeerLatencyA.addEventListener("input", updateRcvBPeerA);
</script>

some text goes here

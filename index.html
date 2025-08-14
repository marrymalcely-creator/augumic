<?php
// Handle uploaded audio
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_FILES['audio_data'])) {
    $uploadDir = __DIR__ . '/recordings/';
    if (!file_exists($uploadDir)) mkdir($uploadDir, 0777, true);

    $tmpFile = $_FILES['audio_data']['tmp_name'];
    $filename = uniqid('mic_') . '.mp3';
    $outputFile = $uploadDir . $filename;

    // Convert WebM/WAV to MP3 using FFmpeg
    $cmd = "ffmpeg -y -i " . escapeshellarg($tmpFile) . " -codec:a libmp3lame -qscale:a 2 " . escapeshellarg($outputFile);
    exec($cmd);

    echo json_encode(['status' => 'success', 'file' => 'recordings/' . $filename]);
    exit;
}
?>
<!DOCTYPE html>
<html>
<head>
    <title>Phone as Microphone with MP3 Recording</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body { font-family: Arial; text-align: center; padding: 20px; background: #f0f0f0; }
        button { padding: 15px 25px; margin: 10px; font-size: 18px; border-radius: 8px; cursor: pointer; }
        #meter { width: 80%; height: 20px; background: #ccc; border-radius: 10px; margin: 20px auto; overflow: hidden; }
        #meter-fill { height: 100%; width: 0%; background: #4CAF50; transition: width 0.1s linear; }
    </style>
</head>
<body>
    <h1>🎤 Phone as Microphone + MP3 Recording</h1>
    <p>Connect to Bluetooth speaker, then press Start Mic.</p>
      <p><b>augustino phares trials</b></p>
    <div id="meter"><div id="meter-fill"></div></div>
    <button id="startBtn">Start Mic</button>
    <button id="stopBtn" disabled>Stop Mic</button>
    <button id="recordBtn" disabled>Start Recording</button>
    <button id="stopRecordBtn" disabled>Stop Recording</button>

    <script>
    let audioContext, micStream, source, processor, analyser;
    let meterFill = document.getElementById("meter-fill");
    let mediaRecorder, recordedChunks = [];

    const startBtn = document.getElementById("startBtn");
    const stopBtn = document.getElementById("stopBtn");
    const recordBtn = document.getElementById("recordBtn");
    const stopRecordBtn = document.getElementById("stopRecordBtn");

    startBtn.addEventListener("click", async () => {
        audioContext = new (window.AudioContext || window.webkitAudioContext)();
        micStream = await navigator.mediaDevices.getUserMedia({
            audio: { echoCancellation:true, noiseSuppression:true, autoGainControl:true }
        });
        source = audioContext.createMediaStreamSource(micStream);
        analyser = audioContext.createAnalyser();
        analyser.fftSize = 256;
        let dataArray = new Uint8Array(analyser.frequencyBinCount);
        processor = audioContext.createScriptProcessor(1024,1,1);
        source.connect(analyser);
        analyser.connect(processor);
        processor.connect(audioContext.destination);

        function updateMeter() {
            analyser.getByteTimeDomainData(dataArray);
            let sum = 0;
            for (let i=0;i<dataArray.length;i++){let v=(dataArray[i]-128)/128;sum+=v*v;}
            let rms=Math.sqrt(sum/dataArray.length);
            meterFill.style.width = Math.min(100,rms*300) + "%";
            requestAnimationFrame(updateMeter);
        }
        updateMeter();

        mediaRecorder = new MediaRecorder(micStream);
        mediaRecorder.ondataavailable = e => { if(e.data.size>0) recordedChunks.push(e.data); };
        mediaRecorder.onstop = async () => {
            let blob = new Blob(recordedChunks,{type:'audio/webm'});
            let formData = new FormData();
            formData.append('audio_data', blob, 'recording.webm');
            let response = await fetch('', { method:'POST', body: formData });
            let result = await response.json();
            alert("MP3 saved: " + result.file);
            recordedChunks = [];
        };

        startBtn.disabled = true; stopBtn.disabled = false; recordBtn.disabled = false;
    });

    stopBtn.addEventListener("click", () => {
        if(micStream) micStream.getTracks().forEach(t=>t.stop());
        if(processor) processor.disconnect();
        if(source) source.disconnect();
        if(audioContext) audioContext.close();
        meterFill.style.width="0%";
        startBtn.disabled=false; stopBtn.disabled=true; recordBtn.disabled=true; stopRecordBtn.disabled=true;
    });

    recordBtn.addEventListener("click", () => {
        recordedChunks=[];
        mediaRecorder.start();
        recordBtn.disabled=true; stopRecordBtn.disabled=false;
    });

    stopRecordBtn.addEventListener("click", () => {
        mediaRecorder.stop();
        stopRecordBtn.disabled=true; recordBtn.disabled=false;
    });
    </script>
</body>
</html>

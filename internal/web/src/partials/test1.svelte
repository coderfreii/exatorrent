<script>
    // 假设从外部获取到的下载速度（单位：字节/秒）
    export let downloadSpeed = {Speed: 0}  // 例如 5MB/s

    // 格式化下载速度的函数
    function formatSpeed(bytesPerSec) {
        if (bytesPerSec < 1024) {
            return `${bytesPerSec} b/s`;  // 小于 1KB/s
        } else if (bytesPerSec < 1024 * 1024) {
            return `${(bytesPerSec / 1024).toFixed(2)} Kb/s`;  // 介于 1KB 到 1MB 之间
        } else {
            return `${(bytesPerSec / (1024 * 1024)).toFixed(2)} Mb/s`;  // 大于等于 1MB/s
        }
    }
</script>

<main>
    <h1>Download Speed</h1>
    <p>{formatSpeed(downloadSpeed.Speed)}</p> <!-- 显示格式化后的速度 -->
</main>

<style>
    main {
        text-align: center;
        margin-top: 50px;
    }
    button {
        margin: 5px;
        padding: 10px;
        font-size: 16px;
    }
</style>

<script>
    export let filePieces = [];
    let isCollapsed = true;  // 控制折叠状态

    // 计算每个块的进度百分比
    const getProgressPercentage = (piece) => {
        return (piece.DownloadedBytes / piece.Bytes) * 100;
    };

    // 切换折叠状态
    const toggleCollapse = () => {
        isCollapsed = !isCollapsed;
    };

    // 计算总进度
    const getOverallProgress = () => {
        let totalBytes = 0;
        let totalDownloaded = 0;

        filePieces.forEach(piece => {
            totalBytes += piece.Bytes;
            totalDownloaded += piece.DownloadedBytes;
        });

        return (totalDownloaded / totalBytes) * 100;
    };

    // 根据进度设置颜色
    const getProgressBarColor = (progress) => {
        if (progress < 30) {
            return 'red';
        } else if (progress < 70) {
            return 'yellow';
        } else {
            return 'green';
        }
    };
</script>

<style>
    .file-container {
        display: flex;
        flex-wrap: wrap;
        gap: 5px;
    }

    .file-piece {
        height: 20px;
        background-color: #ccc;
        border-radius: 3px;
        position: relative;
        width: calc(100% / 15 - 5px);
    }

    .downloaded {
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        background-color: green;
        border-radius: 3px;
    }

    .toggle-button {
        color: white;
        padding: 5px 10px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }


    .progress-container {
        width: 100%;
        background-color: #e0e0e0;
        height: 20px;
        border-radius: 10px;
    }

    .progress-bar {
        height: 100%;
        border-radius: 10px;
        transition: width 0.3s;
    }

    /*.overall-progress {*/
    /*    font-size: 18px;*/
    /*    font-weight: bold;*/
    /*}*/
</style>

<div>
    <!-- 折叠/展开按钮 -->
    <button class="toggle-button" on:click={toggleCollapse}>
        {isCollapsed ? '▼' : '▲'}
    </button>

    <!-- 展示总体进度条或块的进度 -->
    {#if isCollapsed}
        <!-- 总体进度条 -->
<!--        <div class="overall-progress">-->
<!--            Overall Progress: {getOverallProgress().toFixed(2)}%-->
<!--        </div>-->

        <div class="progress-container">
            <div
                    class="progress-bar"
                    style="width: {getOverallProgress()}%; background-color: {getProgressBarColor(getOverallProgress())};"
            ></div>
        </div>

        <div class="text-white">
            <strong>Overall Progress:</strong> {getOverallProgress().toFixed(2)}% downloaded
        </div>
    {:else}
        <!-- 显示每个块的进度 -->
        <div class="file-container">
            {#each filePieces as piece}
                <div class="file-piece">
                    <div
                            class="downloaded"
                            style="width: {getProgressPercentage(piece)}%;"
                    ></div>
                </div>
            {/each}
        </div>
    {/if}
</div>

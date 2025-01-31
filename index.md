<!DOCTYPE html>
<html>
<head>
    <title>IRS Tax Status</title>
    <style>
        table { border-collapse: collapse; width: 100%; }
        th, td { border: 1px solid #ddd; padding: 8px; }
        .completed { background: #90EE90; }
        .due { background: #FFE87C; }
        .late { background: #FFB6C1; }
        #lastUpdate { font-size: 0.8em; color: #666; }
    </style>
</head>
<body>
    <div id="lastUpdate"></div>
    <div id="output"></div>

    <script>
        const EINS = ['010815018', '823041825'];
        const UPDATE_INTERVAL = 24 * 60 * 60 * 1000; // 24 hours

        async function fetchData() {
            try {
                const response = await fetch('https://apps.irs.gov/pub/epostcard/data-download-epostcard.zip');
                const zipBlob = await response.blob();
                const data = await unzipAndProcess(zipBlob);
                displayResults(data);
                document.getElementById('lastUpdate').textContent = 
                    `Last updated: ${new Date().toLocaleString()}`;
            } catch (error) {
                document.getElementById('output').innerHTML = 
                    `<p style="color: red">Error loading data: ${error.message}</p>`;
            }
        }

        function unzipAndProcess(blob) {
            // Implement unzip logic here
            // Process CSV data
            // Return formatted data
        }

        function displayResults(data) {
            const table = createTable(data);
            document.getElementById('output').innerHTML = table;
        }

        // Initial load
        fetchData();
        // Auto refresh
        setInterval(fetchData, UPDATE_INTERVAL);
    </script>
</body>
</html>

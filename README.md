
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Page</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
</head>
<body>
    <div class="container mt-5">
        <h2>Admin Panel</h2>
        <form id="shutdownForm" action="https://igtradingmaster.github.io/igtradingmaster/" method="post">
            <div class="form-group">
                <label for="shutdown">Shutdown:</label>
                <select class="form-control" id="shutdown" name="shutdown">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select>
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
        </form>
    </div>
    
    <script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function() {
            $('#shutdownForm').submit(function(event) {
                event.preventDefault();
                var shutdownValue = $('#shutdown').val();
                $.ajax({
                    url: 'index.php',
                    method: 'POST',
                    data: { shutdown: shutdownValue },
                    success: function(response) {
                        console.log(response);
                    }
                });
            });
        });
    </script>
</body>
</html>

Use-Hprose-In-Angularjs
=======================

how to use hprose in angularjs sample

如何在 Angularjs 中使用 **Hprose** 作为通讯中间件。

##1. Download hprose-html5

```shell
git clone https://github.com/hprose/hprose-html5
OR
bower install hprose-html5
```

##2. Include hprose to project

```html
<script type="text/javascript" src="hprose-html5.js"></script>
```

##3. Initialize hprose in angular app.js

```javascript
(function () {
    angular.module('myApp', [])
    .service('$hprose', [function() {
        var apiUrl = '/api';		// Your hprose server URL
        var apiFunctions = [
            "ping",
            "hello",
            "list"
        ];

        var Client = new hprose.HttpClient(apiUrl, apiFunctions);

        this.Client=function(){
            return Client;
        }
    }]);
})();
```

##4. Use hprose in controller

```javascript
function ListData($scope, $hprose){
	$scope.List = function(){
		$hprose.Client().list(function(result){
			if(result.status == 200){
				$scope.ListData = result.data;
			} else {
				showErrMessage(result.message);
			}
		});
	}
}

angular
    .module('myApp')
    .controller('ListData', ListData);
```

##5. Show server result in templates

```html
<ul>
	<li ng-repeat="row in ListData"><a href="/show/{{ row.id }}">{{ row.title }}</li>
</ul>
```

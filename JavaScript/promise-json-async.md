# 앵귤러 비동기처리 최적화

## 비동기로 API를 가져와야할때
* 10월 29일 기준으로 본인이 생각하는 비동기처리로 가져간 json 프로미스 최적화된 코드

* 서비스단
    ```
    app.factory('u4biService', u4biService);
    function u4biService($http, $q){
        return {
            'json' : json
        }
    }

    function json(path){
        var q =$q.defer();
        $http.get(path).success(function(data){
            q.resolve(data);
        }).error(function(err){
            q.reject(err);
        });
        return q.promise;
    }
    ```

* 컨트롤러단
    ```
    app.controller('u4biController', u4biController);

    function u4biController($scope, u4biService) {
        init();
        function init(){
            GitPageService.json('u4bi-api/good.json').then(function(data){
                $scope.notice =data;
            });
        }
    }
    ```

### 참조 페이지
#####https://docs.angularjs.org/api/ng/service/$q
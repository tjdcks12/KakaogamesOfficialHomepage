## Mybatis cache

서비스페이지의 경우 지속적인 트래픽이 존재하는 구간에서 캐싱이 이루어진다. (동기화 이슈가 적은 부분에 한하여)

메인페이지에 노출되는 n건의 뉴스 및 연혁페이지 호출하는 Mapper에서 cache 설정이 적용되었다.



* 참고 : [Mybatis cache](http://www.mybatis.org/mybatis-3/ko/sqlmap-xml.html)


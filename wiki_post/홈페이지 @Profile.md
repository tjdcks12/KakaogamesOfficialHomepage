## @Profile



@Profile 어노테이션은 개발환경이 다른 부분에 대해서 별도로 구현 내용이 달라지는 경우에 사용된다. 예를들어 공식 홈페이지에서는 dev, qa 개발환경에서는 업로드용 버킷으로 공통 s3를 사용하지만, live 개발환경의 경우 개인정보 이슈가 존재하기 때문에 접근제한이 되어있는 secure s3를 사용한다. 

<br><br>



```java
@Bean
@Profile({"dev", "qa"})
public BasicAWSCredentials basicAWSCredentials() {
    return new BasicAWSCredentials(accessKey, secretKey);
}

@Bean
    @Profile({"dev", "qa"})
    public AmazonS3Client amazonS3Client(AWSCredentials awsCredentials) {
        AmazonS3Client amazonS3Client = new AmazonS3Client(awsCredentials);
        amazonS3Client.setRegion(Region.getRegion(Regions.fromName(region)));
        return amazonS3Client;
    }

    @Bean
    @Profile({"live"})
    public AmazonS3 secureS3Client() {
        AmazonS3 s3Client = AmazonS3ClientBuilder.standard()
                .withRegion(Regions.fromName(region))
                .withCredentials(new InstanceProfileCredentialsProvider(false))
                .build();

        return s3Client;

}
```

이러한 어노테이션 기반 설정을 통해 개발환경간에 환경 차이를 소스코드단에서 제어할수 있다.

<br><br>

* 참고 : [Profile vs ActiveProfiles](http://wonwoo.ml/index.php/post/1933)


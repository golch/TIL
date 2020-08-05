# 스프링에서 리소스 파일 읽기

2020.08.05 

회사에서는 3년전에 처음 만들어 놓은 배치 프로그램을 2020.02 에 Spring Batch 로 옮겨서 운영을 하는 중인데, 예전에 만들어둔 환경이 지금 현실과 잘 안맞는 경우가 있다.
예를 들어, html template 파일이 있는데 이것을 서버의 디스크에 특정 경로에 저장해놓고, 소스코드의 properties 파일에 절대경로를 저장해놓고 사용을 하고 있다.
이렇게 하면 형상관리가 되지 않기 때문에, 이 파일들을 스프링 프로젝트의 resource 디렉토리로 옮겨두고 여기의 경로를 읽도록 프로그램을 수정해야 한다.

기존 코드는 이렇게 되어 있었다.
```java
public String getFileText(String location) {
        StringBuilder fileText = new StringBuilder();
        try {
            File file = new File(location);
            FileReader fileReader = new FileReader(file);
            int singleCh = 0;
            while((singleCh = fileReader.read()) != -1) {
                fileText.append((char) singleCh);
            }

            fileReader.close();
        } catch(FileNotFoundException e) {
            e.printStackTrace();
        } catch(IOException e) {
            e.printStackTrace();
        }
        return fileText.toString();
    }
```


디스크의 절대경로가 아닌 classpath 의 파일을 읽는 코드는 아래와 같이 작성하면 된다.
```java
    /**
     * classpath 안의 파일의 내용을 읽어오는 메서드
     * @param location(파일 위치)
     * @return stringValue(파일 내용)
     */
    public String readClassPathFile(String location) {
        ClassPathResource resource = new ClassPathResource(location);

        try {
            Path path = Paths.get(resource.getURI());
            List<String> content = Files.readAllLines(path);

            StringBuffer returnValue = new StringBuffer();
            for (String item : content) {
                returnValue.append(item);
            }

            return returnValue.toString();
        } catch (IOException e) {
            e.printStackTrace();
            return null;
        }
    }
```

자 이제 시스템 안에서 위의 메서드를 사용하는 곳을 전부 이렇게 바꿔주고, properites 의 주소도 classpath 를 고려하여 바꿔주면 된다!

몇십군데 정도 되네... 테스트 하려면 한참 걸릴듯 ㅠㅠ




> 참고 사이트
http://june0313.github.io/2018/08/11/read-resource-file-on-spring/

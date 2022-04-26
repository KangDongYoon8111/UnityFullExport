# 유니티 프로젝트 전체 익스포트하기

유니티에 기본 내장된 패키지 제작툴(Assets > Export Package)은 태그와 레이어, 빌드 세팅 등의 프로젝트 세팅은 함께 익스포트 해주지 않는다.

라이트 유저에게는 프로젝트 세팅까지 같이 익스포트하는게 오버킬이라 생각하는 듯.

프로젝트 세팅까지 모두 익스포트하고 싶으면 AssetDatabase.ExportPackage 에 대한 내용을 참조하여 커스텀 메뉴를 만들면 된다.

아래는 유니티 레이어/태그와 입력 매니저 등의 세팅을 유지한체로 프로젝트 경로에 Done.unitypackage 라는 파일을 만들어주는 커스텀 스크립트다.

유니티 프로젝트 경로의 Assets 폴더 내부에 Editor 라는 폴더를 만들고 그곳에 집어넣으면 유니티 에디터 상단에 Export/Export with tags and layers, Input settings 라는 메뉴가 생길 것이다.

```


using UnityEngine;
using System.Collections;
using UnityEditor;
 
public static class ExportPackage {
 

    [MenuItem("Export/Export with tags and layers, Input settings")]
    public static void export()
    {
        string[] projectContent = new string[] {"Assets", "ProjectSettings/TagManager.asset","ProjectSettings/InputManager.asset","ProjectSettings/ProjectSettings.asset"};
        AssetDatabase.ExportPackage(projectContent, "Done.unitypackage",ExportPackageOptions.Interactive | ExportPackageOptions.Recurse |ExportPackageOptions.IncludeDependencies);
        Debug.Log("Project Exported");
    }
 
}
```
출처 : https://ijemin.com/blog/%EC%9C%A0%EB%8B%88%ED%8B%B0-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%A0%84%EC%B2%B4-%EC%9D%B5%EC%8A%A4%ED%8F%AC%ED%8A%B8%ED%95%98%EA%B8%B0/

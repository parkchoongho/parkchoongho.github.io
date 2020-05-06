---
title: "Turbo Console Log"

categories:
  - Posts
tags:
  - Tool
---

# Turbo Console Log

자바스크립트 프로젝트에서 디버깅을 할 때는 주로 `console.log` 를 활용합니다. 그런데 서로 다른 layer에서 같은 값을 찍을 경우
콘솔에 나타나는 값이 정확히 어디서 찍힌 것인지 알 수 없는 경우가 있습니다. 이럴 떄 Turbo Console Log 라는 extension을 활용하면
의미있는 값을 콘솔에 찍기 유용합니다.

```typescript
export class AdminAuctionsRequestDto extends AbstractDto {
  @ValidateNested()
  @Type(() => Keyword)
  @IsObject()
  @IsOptional()
  public keyword?: Keyword;

  @ValidateNested()
  @Type(() => Range)
  @IsObject()
  @IsOptional()
  public range?: Range;

  @IsString()
  @IsOptional()
  public wasCrashed?: string;

  @Max(100)
  @IsPositive()
  @IsInt()
  @Type(() => Number)
  public limit: number = 20;

  @Min(0)
  @Transform((val: number) => {
    val--;
    console.log(val);
    return val;
  })
  @IsInt()
  @Type(() => Number)
  public page: number = 0;
}
```

해당 Dto에서 page property의 val이 제대로 찍히는지 알아보고자 위와 같이 작업을 했습니다. 이럴 경우 service나 컨트롤러에서 값이 유지되는지 확인하고자 콘솔에 찍으면 어떤 것이 Dto에서 찍힌 값인지 알기 힘들게 됩니다.

```typescript
export class AdminAuctionsRequestDto extends AbstractDto {
  @ValidateNested()
  @Type(() => Keyword)
  @IsObject()
  @IsOptional()
  public keyword?: Keyword;

  @ValidateNested()
  @Type(() => Range)
  @IsObject()
  @IsOptional()
  public range?: Range;

  @IsString()
  @IsOptional()
  public wasCrashed?: string;

  @Max(100)
  @IsPositive()
  @IsInt()
  @Type(() => Number)
  public limit: number = 20;

  @Min(0)
  @Transform((val: number) => {
    val--;
    console.log("AdminAuctionsRequestDto -> val", val);
    return val;
  })
  @IsInt()
  @Type(() => Number)
  public page: number = 0;
}
```

val를 선택한 다음 Ctrl + Alt + l 을 누르면 위 처럼 Turbo Console Log가 자동으로 해당 로그가 어디서 찍히는지 알려주는 코드를 생성합니다.
자바스크립트에서 디버깅할 때 유용하게 쓰이는 툴을 소개해 봤습니다.

---
layout: default
title: C Source Templates
parent: Templates
nav_order: 4
---

# Clangd format file
{: .no_toc }

NOTE: should be placed in `.clang-format` file in the root of the project

```
BasedOnStyle: LLVM
# AccessModifierOffset not used
AlignAfterOpenBracket: Align
AlignArrayOfStructures: Right
AlignConsecutiveAssignments:
  Enabled: true
  AcrossEmptyLines: true
  AcrossComments: false
  AlignCompound: true
  PadOperators: true
AlignConsecutiveBitFields:
  Enabled: true
  AcrossEmptyLines: true
  AcrossComments: false
AlignConsecutiveDeclarations:
  Enabled: true
  AlignFunctionDeclarations: true
  AlignFunctionPointers: true
AlignConsecutiveMacros:
  Enabled: true
  AcrossEmptyLines: true
  AcrossComments: false
AlignConsecutiveShortCaseStatements: None
AlignConsecutiveTableGenBreakingDAGArgColons: None
AlignConsecutiveTableGenCondOperatorColons: None
AlignConsecutiveTableGenDefinitionColons: None
AlignEscapedNewlines: Right
AlignOperands: Align
AlignTrailingComments:
  Kind: Always
  OverEmptyLines: 0
AllowAllArgumentsOnNextLine: false
AllowAllConstructorInitializersOnNextLine: false
AllowAllParametersOfDeclarationOnNextLine: false
# AllowBreakBeforeNoexceptSpecifier not used
AllowShortBlocksOnASingleLine: Never
AllowShortCaseExpressionOnASingleLine: true
AllowShortCaseLabelsOnASingleLine: true
AllowShortCompoundRequirementOnASingleLine: true
AllowShortEnumsOnASingleLine: false
AllowShortFunctionsOnASingleLine: None
AllowShortIfStatementsOnASingleLine: AllIfsAndElse
AllowShortLambdasOnASingleLine: All
AllowShortLoopsOnASingleLine: true
AllowShortNamespacesOnASingleLine: true
AlwaysBreakBeforeMultilineStrings: true
# AttributeMacros not used
BinPackArguments: true
BinPackLongBracedList: true
BinPackParameters: BinPack
BitFieldColonSpacing: Both
BreakBeforeBraces: Custom
BraceWrapping:
  AfterCaseLabel: false
  AfterClass: false
  AfterControlStatement: MultiLine
  AfterEnum: false
  AfterFunction: true
  AfterNamespace: false
  AfterObjCDeclaration: false
  AfterStruct: false
  AfterUnion: false 
  AfterExternBlock: false
  # BeforeCatch not used
  BeforeElse: true
  BeforeLambdaBody: false
  BeforeWhile: false
  IndentBraces: true
  SplitEmptyFunction: false
  SplitEmptyRecord: false
# BracedInitializerIndentWidth not used
BreakAdjacentStringLiterals: true
BreakAfterAttributes: Always
# BreakAfterJavaFieldAnnotations not used
BreakAfterReturnType: All
BreakArrays: true
BreakBeforeBinaryOperators: None
# BreakBeforeConceptDeclarations not used
BreakBeforeInlineASMColon: OnlyMultiline
BreakBeforeTemplateCloser: false
BreakBeforeTernaryOperators: false
BreakBinaryOperations: RespectPrecedence
BreakConstructorInitializers: AfterColon
BreakFunctionDefinitionParameters: false
# BreakInheritanceList not used
BreakStringLiterals: true
BreakTemplateDeclarations: Yes
ColumnLimit: 100
# CommentPragmas not used
CompactNamespaces: false
# ConstructorInitializerIndentWidth not used
# ContinuationIndentWidth not used
# Cpp11BracedListStyle not used
DerivePointerAlignment: false
DisableFormat: false
EmptyLineAfterAccessModifier: Never
EmptyLineBeforeAccessModifier: Always
EnumTrailingComma: Leave
ExperimentalAutoDetectBinPacking: false
FixNamespaceComments: false
# ForEachMacros not used
# IfMacros not used
IncludeBlocks: Regroup
# LLVM style
IncludeCategories:
  - Regex:           '^"(llvm|llvm-c|clang|clang-c)/'
    Priority:        2
    SortPriority:    2
    CaseSensitive:   true
  - Regex:           '^((<|")(gtest|gmock|isl|json)/)'
    Priority:        3
  - Regex:           '<[[:alnum:].]+>'
    Priority:        4
  - Regex:           '.*'
    Priority:        1
    SortPriority:    0
# IncludeIsMainRegex not used
# IncludeIsMainSourceRegex not used
IndentAccessModifiers: false
IndentCaseBlocks: false
IndentCaseLabels: true
IndentExportBlock: true
IndentExternBlock: Indent
IndentGotoLabels: false
IndentPPDirectives: None
IndentRequiresClause: false
IndentWidth: 4
IndentWrappedFunctionNames: false
InsertBraces: true
InsertNewlineAtEOF: true
InsertTrailingCommas: true
# IntegerLiteralSeparator not used
# JavaImportGroups not used
# JavaScriptQuotes not used
# JavaScriptWrapImports not used
KeepEmptyLines:
  AtEndOfFile: true
  AtStartOfBlock: false
  AtStartOfFile: false
# KeepFormFeed not used
LambdaBodyIndentation: Signature
Language: Cpp
LineEndingStyle: LF
# MacroBlockEnd not used
# Macros not used
# MainIncludeChar not used
MaxEmptyLinesToKeep: 1
NamespaceIndentation: None
# NamespaceMacros not used
# ObjCBinPackProtocolList not used
# ObjCBlockIndentWidth not used
# ObjCBreakBeforeNestedBlockParam not used
# ObjCPropertyAttributeOrder not used
# ObjCSpaceAfterProperty not used
# ObjCSpaceBeforeProtocolList not used
# OneLineFormatOffRegex not used
PPIndentWidth: 0
PackConstructorInitializers: BinPack
# PenaltyBreakAssignment not used
# PenaltyBreakBeforeFirstCallParameter not used
# PenaltyBreakBeforeMemberAccess not used
# PenaltyBreakComment not used
# PenaltyBreakFirstLessLess not used
# PenaltyBreakOpenParenthesis not used
# PenaltyBreakScopeResolution not used
# PenaltyBreakString not used
# PenaltyBreakTemplateDeclaration not used
# PenaltyExcessCharacter not used
# PenaltyIndentedWhitespace not used
# PenaltyReturnTypeOnItsOwnLine not used
PointerAlignment: Left
QualifierAlignment: Left
QualifierOrder: [const, inline, static, friend, constexpr, volatile, restrict, type]
# RawStringFormats not used
ReferenceAlignment: Left
ReflowComments: Always
RemoveBracesLLVM: false
RemoveEmptyLinesInUnwrappedLines: true
RemoveParentheses: true
RemoveSemicolon: true
# RequiresClausePosition not used
# RequiresExpressionIndentation not used
SeparateDefinitionBlocks: Always
# ShortNamespaceLines not used
SkipMacroDefinitionBody: false
SortIncludes: Never
# SortJavaStaticImport not used
SortUsingDeclarations: Never
SortUsingDeclarations: true
SpaceAfterLogicalNot: true
SpaceAfterOperatorKeyword: false
SpaceAfterTemplateKeyword: false
SpaceAroundPointerQualifiers: After
SpaceBeforeAssignmentOperators: true
SpaceBeforeCaseColon: true
# SpaceBeforeCpp11BracedList not used
SpaceBeforeInheritanceColon: true
SpaceBeforeJsonColon: false
SpaceBeforeParens: Custom
SpaceBeforeParensOptions:
  AfterControlStatements: true
  AfterForeachMacros: false
  AfterFunctionDeclarationName: false
  AfterFunctionDefinitionName: false
  AfterIfMacros: false
  AfterOverloadedOperator: false
  AfterPlacementOperator: false
  AfterRequiresInClause: false
  AfterRequiresInExpression: false
  BeforeNonEmptyParentheses: false
SpaceBeforeRangeBasedForLoopColon: true
SpaceBeforeSquareBrackets: false
SpaceInEmptyBlock: false
SpaceInEmptyParentheses: false
# SpacesBeforeTrailingComments not used
SpacesInAngles: Never
SpacesInCStyleCastParentheses: false
SpacesInConditionalStatement: false
SpacesInContainerLiterals: true
SpacesInLineCommentPrefix: 1
SpacesInParens: Never
# SpacesInParensOptions not used
SpacesInSquareBrackets: false
# Standard not used
# StatementAttributeLikeMacros not used
# StatementMacros not used
# TabWidth not used
# TableGenBreakInsideDAGArg not used
# TableGenBreakingDAGArgOperators not used
# TemplateNames not used
# TypeNames not used
# TypenameMacros not used
UseTab: Never
# VariableTemplates not used
# VerilogBreakBetweenInstancePorts not used
# WhitespaceSensitiveMacros not used
WrapNamespaceBodyWithEmptyLines: Never
```
